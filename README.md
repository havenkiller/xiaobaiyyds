# xiaobaiyyds — 超级智能助手

> 全能任务处理中枢 · 框架无关 · 多智能体专家团协作

## 一句话

**小白 yyds** 是你的专属 AI 任务管家。它自动掌握你 skill 库里全部能力，面对任何任务都能智能匹配最合适的 skill 来执行。复杂任务还能启动专家团模式——像一整个产品团队帮你干活。

## 快速安装

```bash
npx skills add <你的GitHub用户名>/xiaobaiyyds
```

或手动克隆：

```bash
git clone https://github.com/<你的GitHub用户名>/xiaobaiyyds.git ~/.claude/skills/xiaobaiyyds
```

## 使用方式

在 Claude Code 中输入 `/xiaobaiyyds` 或直接说：

- "小白，帮我做个海报"
- "呼叫小白，调研一下这个技术方案"
- "帮我完成这个任务"

## 核心能力

- **全库精通** — 自动扫描并彻底掌握所有已安装 skill
- **智能路由** — 根据任务类型自动匹配最合适的 skill
- **专家团协作** — 复杂任务拆解为多角色并行工作流
- **持久记忆** — 跨会话记住交互记录、决策、偏好、踩过的坑
- **自动保存** — 完成任务/发现偏好/做出决策时自动保存到项目记忆

## 依赖

xiaobaiyyds 推荐与以下 skill 配合使用获得最佳体验：

- [gstack](https://github.com/garrytan/gstack) — 项目开发框架
- [superpowers](https://github.com/obra/superpowers) — 超级方法论链

## 项目结构

```
xiaobaiyyds/
├── SKILL.md              ← 核心 skill 定义
├── rule-CLAUDE.md        ← 行为准则
├── references/           ← 参考文档
│   ├── skill-index-schema.md
│   └── team-workflow.md
├── LICENSE               ← MIT 协议
└── README.md
```

## 许可证

MIT
