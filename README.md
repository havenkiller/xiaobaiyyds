# xiaobaiyyds — 技能指挥官

> AI 语义匹配 · 索引驱动 · 原版执行 · 零硬编码

## 一句话

**小白 yyds** 是你 skill 仓库的指挥官。启动时只读轻量索引（~8KB），知道你有什么 skill。你提需求 → AI 理解语义自动匹配最合适的 skill → 你确认 → 调出原版 skill 执行。还能在 dispatch 前深度搜索，让 skill 拿到最新情报。

**没有 tags，没有硬编码，全靠 AI 理解。**

---

## 核心原理

```
旧（v3/v4）:  脚本猜 tags → 关键词匹配 tags → 经常贴错标签
新（v5）:    索引提供 id+name+desc → AI 理解 desc 做语义匹配 → 100% 准
```

索引里只有干净数据，匹配全靠 AI 的理解力。

### v3 → v5 对比

```
v3（旧）                v5（新）
────────────────────    ────────────────────
启动扫全部 SKILL.md      启动只读 .skill-index.json
  80K-120K token         ~8K token  省 90%

脚本猜 tags 分类          AI 语义理解 desc
  容易贴错标签             100% 准确

Skill 工具调子 skill      同左，原汁原味

无搜索前置                Step 2 AQ 询问是否深度搜索
                          → 读 desc 找搜索类 skill
                          → MCP 搜索工具
                          → CLI 搜索命令

永久叠加层                指挥官模式
  想一直留在上下文         用完召回来
```

---

## 工作流程

```
/xiaobaiyyds + 你的需求
    │
    ▼
Step 1  加载 .skill-index.json（~8KB）
    │
    ▼
Step 2  语义匹配（AI 理解，不是关键词匹配）
    ├── 将用户需求与每个 skill 的 name/desc 做语义对比
    ├── 选出最接近的 1-3 个 skill
    └── 若都不相关 → 直接执行，不使用 skill
    │
    ▼
Step 3  AQ：需要先深度搜索最新资料吗？
    ├── 是 → 扫描 desc 理解哪些是搜索类 skill
    │        扫描 MCP 搜索工具
    │        扫描 CLI 搜索命令
    │        全部并行 → 汇总"前沿情报摘要"
    └── 否 → 跳过
    │
    ▼
Step 4  AQ：推荐 skill，用户确认
    ├── "推荐使用：
    │    A) /xxx（功能摘要）
    │    B) /xxx（功能摘要）
    │    C) 直接执行"
    └── 用户选择
    │
    ▼
Step 5  Skill 工具调用原版 skill
    └── 原始需求 + 情报摘要（如有）→ skill 全权执行
```

**核心原则**：用户确认后才能调用 skill。不擅自替用户决定。

---

## 为什么不需要 tags

传统方案需要用脚本给每个 skill 贴标签（search、design、testing...），但脚本模式匹配永远赶不上 AI 的理解力：

```
用户说 "帮我识别这张图里的物体"
  → 读 vision-analysis: "Analyze images using MiniMax vision MCP..."
  → AI 理解 → 匹配成功

用户说 "我想分析商业模式"
  → 读 office-hours: "YC Office Hours partner for product strategy..."
  → AI 理解 → 匹配成功

用户说 "帮我找 bug"
  → 读 investigate: "Systematic debugging with root cause investigation..."
  → AI 理解 → 匹配成功
```

**不需要 tags，不需要分类规则。** 索引只提供原始描述，AI 做所有理解工作。

---

## 索引系统

索引由 `build-index.sh` 自动生成，存放在 `~/.claude/skills/.skill-index.json`。

### 每条记录的格式

```json
{"id":"investigate","desc":"Systematic debugging with root cause investigation...","size":"large"}
```

只有四个字段：
- `id` — 技能目录名
- `name` — 技能标题
- `desc` — 功能描述（AI 匹配的依据）
- `size` / `bytes` — 文件大小

### 索引生成时机

- **首次召唤 /xiaobaiyyds**：自动检测索引不存在 → 自动运行 build-index.sh 生成
- **后续召唤**：直接读已有索引，秒级加载
- **安装新 skill 后**：手动重建

```bash
bash ~/.claude/skills/xiaobaiyyds/bin/build-index.sh
```

---

## 深度搜索

当选择"深度搜索"时，自动发现并调用当前环境所有可用的搜索资源：

| 来源 | 发现方式 |
|------|---------|
| 搜索类 skill | 读 desc，AI 理解哪些是搜索/爬取类 skill |
| MCP 搜索工具 | 检查当前可用的 MCP 工具 |
| CLI 搜索命令 | 检查当前环境的 CLI 命令 |

**有什么用什么。** 不做硬编码假设。

---

## 快速安装

```bash
npx skills add havenkiller/xiaobaiyyds
```

或手动克隆：

```bash
git clone https://github.com/havenkiller/xiaobaiyyds.git ~/.claude/skills/xiaobaiyyds
```

首次召唤时自动生成索引。

---

## 使用方式

在 Claude Code 中输入 `/xiaobaiyyds`：

- `/xiaobaiyyds 帮我分析这个产品的商业模式`
- `呼叫小白，调研这个技术方案的最新发展`
- `小白，我有什么skill可以用？`
- `/xiaobaiyyds 帮我写一份报告，需要先搜最新资料`

---

## 项目结构

```
xiaobaiyyds/
├── SKILL.md              ← 核心 skill 定义（指挥官指令）
├── rule-CLAUDE.md        ← 行为准则
├── README.md
├── bin/
│   └── build-index.sh    ← 索引生成脚本（安装自带）
├── references/           ← 参考文档
├── showcase/             ← 宣传物料
└── LICENSE

系统级文件（自动生成）：
~/.claude/skills/
└── .skill-index.json     ← 114 个技能的索引（~8KB）
```

---

## 设计哲学

- **索引驱动**：只读 ~8KB 索引，不扫全量 SKILL.md
- **AI 语义匹配**：不猜标签、不写死规则，用理解代替匹配
- **零硬编码**：不在代码里写死任何 skill 名称
- **原版执行**：Skill 工具调用，原汁原味
- **情报增强**：需要时先深搜，让决策有前沿依据
- **指挥官模式**：用完召回来，不常驻

---

## 许可证

MIT
