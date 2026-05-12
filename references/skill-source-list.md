# xiaobaiyyds Skill 安装来源汇总

> 整理时间：2026-05-13
> 推荐安装 Skill 总数：**91 个**
> 说明：以下按来源分组，每个 skill 标注了官方安装渠道。你**已经安装**了这些 skill，此文件仅用作查阅和备份。

---

## 一、gstack 开发框架（garrytan/gstack）

**官方仓库**：https://github.com/garrytan/gstack
**安装方式**：
```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup
```

| # | Skill 名称 | 说明 |
|---|-----------|------|
| 1 | `gstack` | 主框架 skill |
| 2 | `autoplan` | 自动审查管道 |
| 3 | `benchmark` | 性能回归检测 |
| 4 | `benchmark-models` | 跨模型基准测试 |
| 5 | `browse` | 快速无头浏览器 QA |
| 6 | `canary` | 部署后金丝雀监控 |
| 7 | `careful` | 破坏性操作安全防护 |
| 8 | `checkpoint` | 工作状态保存/恢复 |
| 9 | `codex` | OpenAI Codex CLI 集成 |
| 10 | `connect-chrome` | 启动 GStack 浏览器 |
| 11 | `context-restore` | 恢复工作上下文 |
| 12 | `context-save` | 保存工作上下文 |
| 13 | `cso` | 首席安全官模式 |
| 14 | `design-consultation` | 设计咨询与系统 |
| 15 | `design-html` | 生产级 HTML/CSS 生成 |
| 16 | `design-review` | 设计师视角 QA |
| 17 | `design-shotgun` | 多方案设计发散 |
| 18 | `devex-review` | 开发者体验审计 |
| 19 | `document-release` | 发布后文档同步 |
| 20 | `freeze` | 限定编辑目录 |
| 21 | `gstack-upgrade` | 升级 gstack |
| 22 | `guard` | 全面安全模式 |
| 23 | `health` | 代码质量仪表盘 |
| 24 | `investigate` | 系统化调试与根因分析 |
| 25 | `land-and-deploy` | 合并+部署工作流 |
| 26 | `landing-report` | PR 队列仪表盘 |
| 27 | `learn` | 项目管理学习记录 |
| 28 | `make-pdf` | Markdown 转 PDF |
| 29 | `office-hours` | YC 模式头脑风暴 |
| 30 | `open-gstack-browser` | 打开 GStack 浏览器 |
| 31 | `pair-agent` | 配对远程 AI 智能体 |
| 32 | `plan-ceo-review` | CEO 模式方案审查 |
| 33 | `plan-design-review` | 设计审查 |
| 34 | `plan-devex-review` | DX 方案审查 |
| 35 | `plan-eng-review` | 工程方案审查 |
| 36 | `plan-tune` | 提问灵敏度调优 |
| 37 | `qa` | 系统化 QA 测试+修复 |
| 38 | `qa-only` | 只报告不修复的 QA |
| 39 | `retro` | 工程周报回顾 |
| 40 | `review` | 合并前 PR 审查 |
| 41 | `scrape` | 网页数据抓取 |
| 42 | `setup-browser-cookies` | 导入浏览器 Cookie |
| 43 | `setup-deploy` | 部署配置 |
| 44 | `setup-gbrain` | gbrain 安装配置 |
| 45 | `ship` | 发布工作流 |
| 46 | `skillify` | 抓取流程固化 |
| 47 | `sync-gbrain` | gbrain 同步 |
| 48 | `unfreeze` | 解除编辑冻结 |

---

## 二、Superpowers 方法论（obra/superpowers）

**官方仓库**：https://github.com/obra/superpowers
**安装方式**：
```bash
# 方式一：官方插件市场安装（推荐）
/plugin install superpowers@claude-plugins-official

# 方式二：自定义市场安装
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

| # | Skill 名称 | 说明 |
|---|-----------|------|
| 1 | `using-superpowers` | 主控 skill |
| 2 | `brainstorming` | 头脑风暴 |
| 3 | `writing-plans` | 编写执行计划 |
| 4 | `executing-plans` | 执行多步计划 |
| 5 | `dispatching-parallel-agents` | 并行智能体调度 |
| 6 | `subagent-driven-development` | 子智能体驱动开发 |
| 7 | `systematic-debugging` | 系统化调试 |
| 8 | `finishing-a-development-branch` | 完成分支合并 |
| 9 | `verification-before-completion` | 完成前验证 |
| 10 | `planning-with-files` | 文件规划（英文） |
| 11 | `planning-with-files-zh` | 文件规划（简体中文） |
| 12 | `planning-with-files-zht` | 文件规划（繁体中文） |
| 13 | `using-git-worktrees` | Git 工作树 |
| 14 | `requesting-code-review` | 请求代码审查 |
| 15 | `receiving-code-review` | 接收代码审查反馈 |
| 16 | `writing-skills` | 编写 Skill |

---

## 三、Anthropic 官方 Skill（anthropics/skills）

**官方仓库**：https://github.com/anthropics/skills
**安装方式**：
```bash
/plugin marketplace add anthropics/skills
# 然后安装对应插件包
/plugin install document-skills@anthropic-agent-skills
/plugin install example-skills@anthropic-agent-skills
```

| # | Skill 名称 | 说明 | 许可证 |
|---|-----------|------|--------|
| 1 | `algorithmic-art` | p5.js 算法艺术 | Apache 2.0 |
| 2 | `brand-guidelines` | Anthropic 品牌规范 | Apache 2.0 |
| 3 | `canvas-design` | 设计哲学视觉创作 | Apache 2.0 |
| 4 | `claude-api` | Claude API/Anthropic SDK 开发指南 | Apache 2.0 |
| 5 | `doc-coauthoring` | 结构化文档协作 | Apache 2.0 |
| 6 | `docx` | Word 文档处理 | Source-Available |
| 7 | `frontend-design` | 生产级前端界面 | Apache 2.0 |
| 8 | `internal-comms` | 内部沟通文档 | Apache 2.0 |
| 9 | `mcp-builder` | MCP 服务器开发指南 | Apache 2.0 |
| 10 | `pdf` | PDF 文件处理 | Source-Available |
| 11 | `pptx` | PowerPoint 处理 | Source-Available |
| 12 | `skill-creator` | 创建/编辑 Skill | Apache 2.0 |
| 13 | `slack-gif-creator` | Slack 动图制作 | Apache 2.0 |
| 14 | `theme-factory` | 预设专业主题 | Apache 2.0 |
| 15 | `web-artifacts-builder` | 复杂 HTML 构建 | Apache 2.0 |
| 16 | `webapp-testing` | Playwright Web 测试 | Apache 2.0 |
| 17 | `xlsx` | Excel 电子表格处理 | Source-Available |

---

## 四、MiniMax Skills 插件市场（MiniMax-AI/skills）

**官方仓库**：https://github.com/MiniMax-AI/skills
**安装方式**：
```bash
/plugin marketplace add minimax-skills
# 或手动配置
git clone https://github.com/MiniMax-AI/skills.git ~/.claude/plugins/marketplaces/minimax-skills
```

已通过插件安装的 Skill（缓存于插件目录）：

| # | Skill 名称 | 说明 |
|---|-----------|------|
| 1 | `minimax-pdf` | PDF 生成（封面+正文+合并） |
| 2 | `minimax-docx` | Word 文档处理 |
| 3 | `minimax-xlsx` | Excel 处理 |
| 4 | `minimax-multimodal-toolkit` | 多模态工具包 |
| 5 | `minimax-music-gen` | 音乐生成 |
| 6 | `minimax-music-playlist` | 音乐播放列表 |
| 7 | `minimax-multimodal-toolkit` | 多模态工具包 |
| 8 | `frontend-dev` | 前端开发 |
| 9 | `fullstack-dev` | 全栈开发 |
| 10 | `flutter-dev` | Flutter 开发 |
| 11 | `android-native-dev` | Android 原生开发 |
| 12 | `ios-application-dev` | iOS 应用开发 |
| 13 | `buddy-sings` | 唱歌机器人 |
| 14 | `gif-sticker-maker` | GIF 贴纸制作 |
| 15 | `pptx-generator` | PPT 生成 |
| 16 | `pr-review` | PR 审查 |

> 注：MiniMax 的 skill 通过插件系统管理，不直接安装在 `~/.claude/skills/` 目录中，但可通过 `/plugin` 命令调用。

---

## 五、独立第三方 Skill

### 5.1 Agent Browser（Vercel Labs）

**官方仓库**：https://github.com/vercel-labs/agent-browser
**安装方式**：
```bash
npm install -g agent-browser && agent-browser install
# 或：npx skills add vercel-labs/agent-browser --skill agent-browser
```
| Skill | `agent-browser` |
|-------|----------------|
| 说明 | AI 专属命令行浏览器自动化工具，Snapshot+Refs 工作流，93% 更少上下文 |

### 5.2 Firecrawl 搜索（firecrawl/cli）

**官方仓库**：https://github.com/firecrawl/cli
**安装方式**：
```bash
npx -y firecrawl-cli@latest init -y --browser
# 或：/plugin install firecrawl@claude-plugins-official
```
| Skill | `firecrawl-search` |
|-------|-------------------|
| 说明 | 全页内容提取的深度网络搜索 |

### 5.3 Tavily 搜索（tavily-ai/skills）

**官方仓库**：https://github.com/tavily-ai/skills
**安装方式**：
```bash
npx skills add https://github.com/tavily-ai/skills
# 先安装 CLI：curl -fsSL https://cli.tavily.com/install.sh | bash
```
| Skill | `tavily-search` |
|-------|----------------|
| 说明 | LLM 优化的网络搜索结果 |

### 5.4 UI/UX Pro Max（nextlevelbuilder）

**官方仓库**：https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
**安装方式**：
```bash
npm install -g uipro-cli && uipro init --ai claude
# 或：npx skills add nextlevelbuilder/ui-ux-pro-max-skill --skill ui-ux-pro-max
# 或：/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
```
| Skill | `ui-ux-pro-max` |
|-------|----------------|
| 说明 | UI/UX 设计智能，50+ 风格、161 调色板、57 字体配对 |

### 5.5 Web Design Engineer（ConardLi/garden-skills）

**官方仓库**：https://github.com/ConardLi/garden-skills
**安装方式**：
```bash
/plugin marketplace add ConardLi/web-design-skill
/plugin install web-design-skills@agent-skills
```
| Skill | `web-design-engineer` |
|-------|----------------------|
| 说明 | 高质量 Web 视觉设计，反 AI 俗套原则 |

### 5.6 Pentest 渗透测试（Transilience AI）

**官方仓库**：https://github.com/transilienceai/communitytools
**安装方式**：
```bash
git clone https://github.com/transilienceai/communitytools.git
# 或使用 Kali Docker：bash scripts/kali-claude-setup.sh projects/pentest
```
| Skill | `pentest` |
|-------|-----------|
| 说明 | 高级渗透测试与黑客技术，27 skill + Kali Docker + HexStrike MCP |

### 5.7 Find Skills（Vercel Labs）

**官方仓库**：https://github.com/vercel-labs/skills
**安装方式**：
```bash
npx skills add vercel-labs/skills@find-skills -g -y
```
| Skill | `find-skills` |
|-------|--------------|
| 说明 | 元 skill，帮助发现和安装其他 skill |

### 5.8 Claude-Mem（thedotmack）

**官方仓库**：https://github.com/thedotmack/claude-mem
**安装方式**：
```bash
git clone https://github.com/thedotmack/claude-mem.git ~/.claude/plugins/claude-mem
cd ~/.claude/plugins/claude-mem && ./install
```
| Skill | `claude-mem` |
|-------|-------------|
| 说明 | 跨会话记忆压缩系统，v12.3.8 |

### 5.9 TDD Skill（社区）

| Skill | 来源 | 安装方式 |
|-------|------|----------|
| `test-driven-development` | 社区（来源于 superpowers 生态） | 随 superpowers 安装 |

### 5.10 Agent Reach（Panniantong）

**官方仓库**：https://github.com/Panniantong/Agent-Reach
**Stars**：⭐ 19,325 · **MIT 开源许可** · 完全免费
**安装方式**：
```bash
npx skills add https://github.com/Panniantong/Agent-Reach -g
pip install agent-reach
agent-reach install --env=auto
```
| Skill | `agent-reach` |
|-------|--------------|
| 说明 | 全平台信息触达 Agent — 搜索/社交/开发/视频/网页/公众号/RSS 全覆盖，17 个平台零配置直连 |

---
---

## 汇总统计

| 来源 | 数量 | 安装方式 |
|------|------|----------|
| gstack（garrytan/gstack） | 48 | `git clone` + `./setup` |
| Superpowers（obra/superpowers） | 16 | `/plugin install` |
| Anthropic 官方（anthropics/skills） | 17 | `/plugin marketplace add` |
| MiniMax Skills | ~16 | `/plugin marketplace add` |
| Agent Browser（Vercel Labs） | 1 | `npm install -g` |
| Firecrawl | 1 | `npx firecrawl-cli` |
| Tavily | 1 | `npx skills add` |
| UI/UX Pro Max | 1 | `npm install -g uipro-cli` |
| Web Design Engineer | 1 | `/plugin marketplace add` |
| Pentest（Transilience AI） | 1 | `git clone` |
| Find Skills（Vercel Labs） | 1 | `npx skills add` |
| Claude-Mem | 1 | `git clone` |
| Agent Reach（Panniantong） | 1 | `npx skills add` + `pip install` |
| 本地/社区自定义 | 4 | 无远程仓库 |
| **总计** | **~91** | |

---

## 关键词快速索引

想找某个 skill 的安装来源？按名称查询：

| Skill 名称 | 所属来源 |
|-----------|---------|
| agent-browser | 五.1 Vercel Labs |
| agent-reach | 五.10 Panniantong |
| algorithmic-art | 三 Anthropic 官方 |
| autoplan | 一 gstack |
| benchmark / benchmark-models | 一 gstack |
| brainstorming | 二 Superpowers |
| brand-guidelines | 三 Anthropic 官方 |
| browse | 一 gstack |
| canary | 一 gstack |
| canvas-design | 三 Anthropic 官方 |
| careful | 一 gstack |
| checkpoint | 一 gstack |
| claude-api | 三 Anthropic 官方 |
| claude-mem | 五.8 thedotmack |
| codex | 一 gstack |
| connect-chrome | 一 gstack |
| context-restore / context-save | 一 gstack |
| cso | 一 gstack |
| design-consultation / design-html / design-review / design-shotgun | 一 gstack |
| devex-review | 一 gstack |
| dispatching-parallel-agents | 二 Superpowers |
| doc-coauthoring | 三 Anthropic 官方 |
| document-release | 一 gstack |
| docx | 三 Anthropic 官方 |
| executing-plans | 二 Superpowers |
| find-skills | 五.7 Vercel Labs |
| finishing-a-development-branch | 二 Superpowers |
| firecrawl-search | 五.2 Firecrawl |
| freeze | 一 gstack |
| frontend-design | 三 Anthropic 官方 |
| gstack / gstack-upgrade | 一 gstack |
| guard | 一 gstack |
| health | 一 gstack |
| internal-comms | 三 Anthropic 官方 |
| investigate | 一 gstack |
| land-and-deploy / landing-report | 一 gstack |
| learn | 一 gstack |
| make-pdf | 一 gstack |
| mcp-builder | 三 Anthropic 官方 |
| office-hours | 一 gstack |
| open-gstack-browser | 一 gstack |
| pair-agent | 一 gstack |
| pdf | 三 Anthropic 官方 |
| pentest | 五.6 Transilience AI |
| plan-ceo-review / plan-design-review / plan-devex-review / plan-eng-review / plan-tune | 一 gstack |
| planning-with-files / planning-with-files-zh / planning-with-files-zht | 二 Superpowers |
| pptx | 三 Anthropic 官方 |
| qa / qa-only | 一 gstack |
| receiving-code-review / requesting-code-review | 二 Superpowers |
| retro | 一 gstack |
| review | 一 gstack |
| scrape | 一 gstack |
| setup-browser-cookies / setup-deploy / setup-gbrain | 一 gstack |
| ship | 一 gstack |
| skill-creator | 三 Anthropic 官方 |
| skillify | 一 gstack |
| slack-gif-creator | 三 Anthropic 官方 |
| subagent-driven-development | 二 Superpowers |
| sync-gbrain | 一 gstack |
| systematic-debugging | 二 Superpowers |
| tavily-search | 五.3 Tavily |
| test-driven-development | 二 Superpowers 生态 |
| theme-factory | 三 Anthropic 官方 |
| ui-ux-pro-max | 五.4 nextlevelbuilder |
| unfreeze | 一 gstack |
| using-git-worktrees | 二 Superpowers |
| using-superpowers | 二 Superpowers |
| verification-before-completion | 二 Superpowers |
| web-artifacts-builder | 三 Anthropic 官方 |
| web-design-engineer | 五.5 ConardLi |
| webapp-testing | 三 Anthropic 官方 |
| writing-plans | 二 Superpowers |
| writing-skills | 二 Superpowers |
| xlsx | 三 Anthropic 官方 |
