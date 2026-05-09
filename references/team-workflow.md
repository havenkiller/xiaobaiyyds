# 专家团协作工作流

## 概述

xiaobaiyyds 的专家团模式是基于 `subagent-driven-development`、`using-superpowers` 和 `gstack` 的高级协作框架。当面对复杂任务时，系统会启动多个专业化角色协同工作，确保任务高效、高质量完成。

---

## 角色定义

### 核心角色

| 角色 | 职责 | 调用的 Skill |
|------|------|-------------|
| **Coordinator** | 主控协调，任务分解，结果汇总 | xiaobaiyyds (主控) |
| **Domain Expert** | 领域专家，负责专项任务 | gstack skill, frontend-dev 等 |
| **Code Reviewer** | 代码审查，质量把关 | gstack/review, gstack/investigate |
| **QA Engineer** | 测试验证，质量保证 | gstack/qa, gstack/browse |
| **Planner** | 规划分解，任务编排 | brainstorming, writing-plans |
| **Ship Engineer** | 部署发布，版本管理 | gstack/ship, gstack/land-and-deploy |

### 扩展角色（按需启用）

| 角色 | 职责 | 触发条件 |
|------|------|----------|
| **Researcher** | 研究调研，信息收集 | 任务涉及未知领域 |
| **Designer** | 界面设计，视觉方案 | 需要 UI/UX 设计 → gstack/design-consultation |
| **Doc Writer** | 文档编写，技术文档 | 需要产出文档 → gstack/document-release |
| **Safety Guard** | 安全防护，破坏性操作警告 | 涉及 rm -rf 等 → gstack/careful |

---

## 协作模式

### 模式 A：完全自动协作

**触发条件**：用户明确要求"自动处理"或"你决定怎么协作"

**流程**：
```
用户输入 → Coordinator 分析 → 自动决定角色组合 → 并行执行 → 汇总交付
```

**优点**：快速，无需等待用户确认
**缺点**：用户失去控制权

---

### 模式 B：始终询问（当前设置）

**触发条件**：检测到复杂任务

**流程**：
```
用户输入 → Coordinator 分析
        ↓
    检测到复杂任务
        ↓
    [询问对话框]
    ┌─────────────────────────────────────┐
    │  检测到复杂任务：XXX                  │
    │  需要协调：角色A, 角色B, 角色C        │
    │  是否启用专家团协作模式？              │
    │                                       │
    │  [ ] 启用多智能体协作（推荐）          │
    │  [ ] 我自己来处理（串行模式）           │
    └─────────────────────────────────────┘
        ↓
用户选择
        ↓
├─ 启用 → 启动专家团 → 并行执行 → 汇总
└─ 拒绝 → 串行执行 → 逐步处理
```

**优点**：用户保持完全控制
**缺点**：需要用户参与决策

---

### 模式 C：按任务类型区分

**触发条件**：预设的任务类型规则

| 任务类型 | 默认模式 | 说明 |
|----------|----------|------|
| `creation:simple` | 自动单 Skill | 创建单个简单文件 |
| `creation:complex` | 询问协作 | 多组件/多领域创建 |
| `modification` | 询问协作 | 涉及多文件修改 |
| `research` | 自动协作 | 研究类任务天然适合并行 |
| `workflow` | 始终协作 | 管理协调类任务 |

---

## 完整工作流

### Phase 1：任务分析 (Coordinator)

**输入**：用户原始需求

**处理**：
1. 理解任务目标和成功标准
2. 识别任务类型（creation/modification/research/workflow）
3. 评估复杂度（简单/复杂）
4. 确定所需技能领域
5. 制定协作策略

**输出**：
```json
{
  "taskSummary": "创建电商产品展示页面",
  "taskType": "creation:complex",
  "complexity": "high",
  "requiredDomains": ["frontend", "design"],
  "collaborationStrategy": "team-with-consultation",
  "subtasks": [
    {"id": 1, "domain": "design", "description": "设计视觉方案"},
    {"id": 2, "domain": "frontend", "description": "实现页面结构"},
    {"id": 3, "domain": "frontend", "description": "实现交互动效"}
  ]
}
```

---

### Phase 2：规划分解 (Planner) - Superpowers Chain

**输入**：Coordinator 的任务分析

**处理**（Superpowers Chain）：
1. **brainstorming** → 理解问题空间，明确目标
   - 调用 `brainstorming` skill
   - 探索问题空间
   - 定义范围和约束
2. **writing-plans** → 创建结构化实施计划
   - 调用 `writing-plans` skill
   - 细化每个子任务
   - 确定依赖关系
   - 估算工作量
3. **dispatching-parallel-agents** → 并行执行独立任务（如有）

**输出**：
```
## 实施计划

### 1. 设计阶段
- [ ] 创建设计规范文档 (gstack/design-consultation)
- [ ] 确定配色方案和字体
- [ ] 产出设计稿

### 2. 前端开发
- [ ] 搭建项目结构
- [ ] 实现 HeroSection
- [ ] 实现 ProductGrid
- [ ] 添加动画效果

### 3. 集成测试
- [ ] 功能测试 (gstack/qa)
- [ ] 响应式测试 (gstack/browse)
- [ ] 性能测试

### 4. 文档交付
- [ ] 编写使用说明 (gstack/document-release)
- [ ] 更新 README
```

---

### Phase 3：并行执行 (Domain Experts)

**输入**：分解后的任务列表

**执行策略**：
- **独立任务**：使用 `dispatching-parallel-agents` 并行执行
- **依赖任务**：按顺序执行，等待前置任务完成

**并行示例**：
```
Agent-1: 设计专家 → 输出设计方案
Agent-2: 前端专家 → 基于设计实现页面
Agent-3: QA工程师 → 同步准备测试用例
         ↓
     设计完成 → 前端开始开发
         ↓
     开发完成 → QA 进行测试
```

**依赖处理**：
```
Task-A (独立) ─┬─→ Task-C (依赖A,B)
Task-B (独立) ─┘
                    ↓
               Task-D (依赖C)
```

---

### Phase 4：质量把关 (Code Reviewer)

**输入**：各专家产出的代码/文档

**处理**：
1. 调用 `gstack/review` 进行代码审查
2. 调用 `gstack/investigate` 进行问题调查（如有 bug）
3. 检查代码质量、安全性、性能
4. 验证是否符合需求
5. 提出改进建议

**输出**：
```json
{
  "reviews": [
    {
      "expert": "gstack/review",
      "output": "HeroSection.tsx",
      "issues": [],
      "score": 9,
      "approved": true
    }
  ]
}
```

---

### Phase 5：测试验证 (QA Engineer)

**输入**：各专家的产出物

**处理**：
1. 调用 `gstack/qa` 执行浏览器自动化测试
2. 调用 `gstack/browse` 进行页面验证
3. 跨浏览器/设备测试
4. 性能和安全扫描
5. 如只需报告不修复，调用 `gstack/qa-only`

**输出**：
```json
{
  "testResults": {
    "functional": "PASS",
    "responsive": "PASS",
    "performance": "PASS",
    "security": "PASS"
  },
  "coverage": "85%"
}
```

---

### Phase 6：结果汇总 (Coordinator)

**输入**：所有角色的输出

**处理**：
1. 收集各专家的产出
2. 整合形成最终交付物
3. 编写执行总结
4. 反馈给用户

**输出**：
```
## 任务完成总结

### 产出物
- 产品展示页面（HTML + CSS + JS）
- 设计规范文档
- 测试报告

### 执行统计
- 总耗时：45 分钟
- 并行任务：3 个
- 代码审查：1 次通过

### 质量评估
- 功能完整性：100%
- 代码质量：9/10
- 测试覆盖率：85%
```

---

## Agent 指令模板

### Coordinator 指令

```markdown
# Coordinator 角色

你是一个任务协调专家（Coordinator）。

## 你的职责
1. 理解用户需求并分解任务
2. 分析任务复杂度
3. 确定需要的专家角色
4. 协调各专家的工作
5. 汇总最终结果

## 当前任务
{TASK_DESCRIPTION}

## 执行策略
{COLLABORATION_STRATEGY}

## 输出格式
按以下格式输出任务分析：
```
任务摘要：
任务类型：
所需角色：
子任务列表：
协作建议：
```
```

### Domain Expert 指令

```markdown
# Domain Expert 角色

你是一个{DOMAIN}领域专家。

## 你的职责
1. 接收 Coordinator 分配的任务
2. 使用你的专业知识完成任务
3. 及时报告进度和问题
4. 交付高质量的产出

## 分配的任务
{TASK_DESCRIPTION}

## 约束条件
- 使用 {SKILL} 进行工作
- 遵循 {GUIDELINES}
- 保持与 Coordinator 的沟通

## 输出要求
完成时提供：
- 产出物列表
- 遇到的问题（如果有）
- 质量自评
```

---

## 沟通机制

### 状态同步

| 事件 | 通知方式 | 内容 |
|------|----------|------|
| 任务开始 | 日志 | `[{role}] 开始执行: {task}` |
| 任务完成 | 日志 | `[{role}] 完成: {task} ({duration})` |
| 发现问题 | 警告 | `[{role}] 问题: {issue}` |
| 需要帮助 | 请求 | `[{role}] 请求协助: {help_needed}` |
| 阻塞等待 | 等待 | `[{role}] 等待: {dependency}` |

### 结果传递

使用结构化的 JSON 格式在 Agent 之间传递结果：

```json
{
  "from": "designer",
  "to": "coordinator",
  "type": "task_complete",
  "taskId": "design-1",
  "output": {
    "files": ["design-spec.md", "mockup.png"],
    "summary": "已完成设计方案"
  },
  "metadata": {
    "duration": "5m",
    "quality": "high"
  }
}
```

---

## 冲突处理

### 冲突类型

| 类型 | 场景 | 处理方式 |
|------|------|----------|
| **资源冲突** | 两个专家需要同一文件 | 锁机制，串行访问 |
| **技术分歧** | 专家间方案不一致 | Coordinator 决策 |
| **优先级冲突** | 任务优先级不明确 | 用户确认 |

### 解决流程

```
检测到冲突
    ↓
收集各方观点
    ↓
Coordinator 分析
    ↓
├─ 能决策 → 直接决定
└─ 不能决策 → 询问用户
    ↓
应用解决方案
```

---

## 最佳实践

### 1. 任务分解粒度
- 每个子任务理想时长：15-30 分钟
- 避免过细分解（增加协调成本）
- 避免过粗分解（降低并行度）

### 2. 并行度控制
- 最佳并行数：3-5 个 Agent
- 超过 5 个时考虑分组
- 保持核心角色始终活跃

### 3. 通信效率
- 使用结构化格式减少歧义
- 关键决策点及时同步
- 避免不必要的信息传递

### 4. 质量门禁
- 每个角色设置质量标准
- 不达标不进入下一阶段
- 记录问题便于追溯

---

## 监控与日志

### 实时监控

```
[10:30:15] Coordinator: 任务开始 - 创建电商产品页
[10:30:16] Coordinator: 分解完成，3 个子任务
[10:30:17] Designer: 开始执行 - 设计视觉方案
[10:30:17] Frontend-Dev: 开始执行 - 实现页面结构
[10:30:17] QA-Engineer: 开始执行 - 准备测试用例
[10:32:45] Designer: 完成 - 设计方案已交付
[10:35:22] Frontend-Dev: 依赖满足，开始实现动效
[10:38:10] QA-Engineer: 测试用例准备完成
[10:40:55] Frontend-Dev: 完成 - 页面实现完成
[10:41:02] QA-Engineer: 开始功能测试
[10:45:30] QA-Engineer: 测试完成 - 全部通过
[10:45:35] Coordinator: 任务完成，汇总交付
```

### 关键指标

| 指标 | 计算方式 | 目标值 |
|------|----------|--------|
| 并行效率 | 实际并行时间 / 总时间 | > 60% |
| 一次通过率 | 无需返工的产出 / 总产出 | > 80% |
| 阻塞时间比 | 阻塞时间 / 总时间 | < 10% |
| 角色利用率 | 角色活跃时间 / 总时间 | > 70% |

---

## gstack Skill 快速索引

### 场景 → Skill 映射

| 场景 | 自动路由 | 手动触发 |
|------|----------|----------|
| 产品构思 | → office-hours | `/office-hours` |
| 战略评审 | → plan-ceo-review | `/plan-ceo-review` |
| 架构设计 | → plan-eng-review | `/plan-eng-review` |
| 设计系统 | → design-consultation | `/design-consultation` |
| 代码审查 | → review | `/review` |
| Bug 调查 | → investigate | `/investigate` |
| 浏览器测试 | → qa | `/qa` |
| 部署发布 | → ship | `/ship` |
| 破坏性操作 | → careful | `/careful` |
| 上下文保存 | → context-save | `/context-save` |

### 完整 gstack Skill 列表

| Category | Skills |
|----------|--------|
| 产品与战略 | office-hours, plan-ceo-review, plan-eng-review, plan-design-review, plan-devex-review |
| 设计与视觉 | design-consultation, design-review, design-html, design-shotgun |
| 代码与调试 | review, investigate, debug, pair-agent |
| 测试与 QA | qa, qa-only, browse |
| 部署与发布 | ship, land-and-deploy, document-release, retro |
| 安全与保护 | careful, freeze, guard, unfreeze |
| 上下文与记忆 | context-save, context-restore |
| 升级与工具 | gstack-upgrade, setup-browser-cookies, setup-deploy, health |
