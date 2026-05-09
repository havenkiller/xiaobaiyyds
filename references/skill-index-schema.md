# Skill Index Schema 详解

## 文件位置

- **项目级**：`./.skill-index.json`（提交到 git，与项目一起版本化）
- **全局级**：`~/.claude/.skill-index.json`（本机所有项目共享）

## 完整 Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "required": ["version", "updated", "skills"],
  "properties": {
    "version": {
      "type": "string",
      "pattern": "^\\d+\\.\\d+\\.\\d+$",
      "description": "索引格式版本，遵循 semver"
    },
    "updated": {
      "type": "string",
      "format": "date-time",
      "description": "最后扫描时间，ISO 8601 格式"
    },
    "scanPaths": {
      "type": "array",
      "items": { "type": "string" },
      "description": "本次扫描的所有路径"
    },
    "skills": {
      "type": "array",
      "items": { "$ref": "#/definitions/skillEntry" }
    },
    "metadata": {
      "type": "object",
      "properties": {
        "totalCount": { "type": "integer" },
        "categoryCounts": {
          "type": "object",
          "additionalProperties": { "type": "integer" }
        }
      }
    }
  },
  "definitions": {
    "skillEntry": {
      "type": "object",
      "required": ["name", "path", "description"],
      "properties": {
        "name": {
          "type": "string",
          "description": "Skill 名称，必须唯一"
        },
        "path": {
          "type": "string",
          "description": "SKILL.md 的绝对路径"
        },
        "description": {
          "type": "string",
          "description": "Skill 描述，用于匹配和展示"
        },
        "category": {
          "type": "string",
          "enum": ["frontend", "backend", "fullstack", "mobile", "document", "media", "meta", "tool"],
          "description": "技能分类"
        },
        "keywords": {
          "type": "array",
          "items": { "type": "string" },
          "description": "关键词列表，增强匹配精度"
        },
        "triggerPhrases": {
          "type": "array",
          "items": { "type": "string" },
          "description": "触发短语，当用户输入这些词时优先匹配"
        },
        "requiredTools": {
          "type": "array",
          "items": { "type": "string" },
          "description": "skill 需要使用的工具列表"
        },
        "compatibility": {
          "type": "object",
          "properties": {
            "claudecode": { "type": "boolean" },
            "openclaw": { "type": "boolean" },
            "claudeai": { "type": "boolean" }
          }
        }
      }
    }
  }
}
```

## 字段说明

### 必填字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `name` | string | Skill 名称，需全局唯一 |
| `path` | string | SKILL.md 的绝对路径 |
| `description` | string | 完整描述，将用于匹配 |

### 可选字段

| 字段 | 类型 | 说明 | 示例 |
|------|------|------|------|
| `category` | enum | 技能分类 | `"frontend"`, `"backend"`, `"meta"` |
| `keywords` | string[] | 关键词数组 | `["react", "vue", "ui"]` |
| `triggerPhrases` | string[] | 触发短语 | `["创建前端", "/frontend-dev"]` |
| `requiredTools` | string[] | 所需工具 | `["Read", "Write", "Bash"]` |
| `compatibility` | object | 框架兼容性 | `{"claudecode": true}` |

## 示例

### 最小示例

```json
{
  "version": "1.0.0",
  "updated": "2026-05-07T10:00:00Z",
  "skills": [
    {
      "name": "my-skill",
      "path": "/Users/xos/.claude/skills/my-skill/SKILL.md",
      "description": "我的自定义技能"
    }
  ]
}
```

### 完整示例

```json
{
  "version": "1.0.0",
  "updated": "2026-05-07T10:00:00Z",
  "scanPaths": [
    "/Users/xos/.claude/skills",
    "/Users/xos/.claude/plugins/cache/minimax-skills/1.0.0/skills"
  ],
  "skills": [
    {
      "name": "frontend-dev",
      "path": "/Users/xos/.claude/plugins/cache/minimax-skills/1.0.0/skills/frontend-dev/SKILL.md",
      "description": "Full-stack frontend development combining premium UI design, cinematic animations...",
      "category": "frontend",
      "keywords": ["react", "next.js", "tailwind", "animation", "gsap", "framer-motion"],
      "triggerPhrases": ["创建前端页面", "build a landing page", "/frontend-dev"],
      "requiredTools": ["Read", "Write", "Bash", "Glob"],
      "compatibility": {
        "claudecode": true,
        "openclaw": true,
        "claudeai": true
      }
    },
    {
      "name": "skill-creator",
      "path": "/Users/xos/.claude/skills/skill-creator/SKILL.md",
      "description": "Create new skills, modify and improve existing skills...",
      "category": "meta",
      "keywords": ["skill", "create", "improve", "benchmark", "eval"],
      "triggerPhrases": ["创建 skill", "/skill-creator", "make a skill"],
      "requiredTools": ["Read", "Write", "Glob", "Grep"],
      "compatibility": {
        "claudecode": true,
        "openclaw": false,
        "claudeai": true
      }
    }
  ],
  "metadata": {
    "totalCount": 2,
    "categoryCounts": {
      "frontend": 1,
      "meta": 1
    }
  }
}
```

## 扫描路径配置

xiaobaiyyds 默认扫描以下路径：

```javascript
const DEFAULT_SCAN_PATHS = [
  // 用户本地 skill 库
  `${HOME}/.claude/skills`,
  // minimax-skills 插件
  `${HOME}/.claude/plugins/cache/minimax-skills/**/skills`,
  // 项目内 skill（当前目录）
  `./skills`,
  `./.claude/skills`
];
```

## 索引生成流程

```
1. 扫描所有 SKILL.md 文件
        ↓
2. 解析每个文件的 frontmatter
        ↓
3. 提取 name, description, category, keywords
        ↓
4. 合并到统一结构
        ↓
5. 计算 metadata (totalCount, categoryCounts)
        ↓
6. 写入 .skill-index.json
```

## 版本兼容性

| 版本 | 支持的 schema | 说明 |
|------|---------------|------|
| 1.0.0 | draft-07 | 初始版本 |

未来升级时会在 `version` 字段体现，xiaobaiyyds 会检测版本并提示迁移。
