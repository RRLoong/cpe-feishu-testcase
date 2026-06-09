---
name: create-rule
description: >-
  Guides creation of Cursor project rules (.mdc) for CPE router/ONT testing
  repos. Use when adding .cursor/rules/, testcase conventions, globs for
  automation or markdown, or asking about alwaysApply vs file-scoped rules.
disable-model-invocation: true
---

# Create Rule（CPE 测试团队）

在本仓库或关联测试项目中创建 `.cursor/rules/*.mdc`。

## Phase 1：收集需求

| 项 | 说明 |
|----|------|
| 目的 | 约束用例格式、缺陷字段、自动化风格、日志脱敏 |
| 作用域 | `alwaysApply: true` 或 `globs` 文件匹配 |
| 模式 | 例如 `**/*.md`（用例）、`**/*.robot`、`**/tests/**/*.py` |

**未说明作用域时**：先问「全局生效还是仅特定文件？」

### CPE 常用 globs

| 内容 | 建议 glob |
|------|-----------|
| 测试用例 Markdown | `**/testcases/**/*.md`, `**/*用例*.md` |
| Robot Framework | `**/*.robot` |
| Python 自动化 | `**/tests/**/*.py`, `**/automation/**/*.py` |
| Skill 文件 | `**/.cursor/skills/**/SKILL.md` |
| Rule 文件 | `.cursor/rules/**/*.mdc` |

## Phase 2：设计

- **一条规则一个主题**，正文建议 <50 行（硬上限 500）。
- **可执行**：写清 ✅/❌ 对照，避免空泛原则。
- **与 Skill 分工**：Rule = 长期格式/禁忌；Skill = 完整分步工作流。

从模板复制：[templates/rule-skeleton.mdc](templates/rule-skeleton.mdc)

## Phase 3：实现

路径：`.cursor/rules/<kebab-name>.mdc`

```markdown
---
description: One line for rule picker
globs: "**/testcases/**/*.md"
alwaysApply: false
---

# Rule Title

内容...
```

仅全局约束时：

```yaml
---
description: ...
alwaysApply: true
---
```

## Phase 4：验收

- [ ] 扩展名为 `.mdc`，frontmatter 合法
- [ ] `alwaysApply` 与 `globs` 不冲突（file-scoped 时 `alwaysApply: false`）
- [ ] 无密钥与真实客户数据
- [ ] 含至少一组 ✅/❌ 示例

## 本仓库已装规则

| 文件 | 作用 |
|------|------|
| `cpe-repo-core.mdc` | 仓库通用约束（始终生效） |
| `skill-authoring.mdc` | 编辑 Skill 时生效 |
| `rule-authoring.mdc` | 编辑 Rule 时生效 |

## 资源

- 官方：Cursor 内置 `create-rule`（`~/.cursor/skills-cursor/create-rule/`）
- 模板：[templates/rule-skeleton.mdc](templates/rule-skeleton.mdc)
