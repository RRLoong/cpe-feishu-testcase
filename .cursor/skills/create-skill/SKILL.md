---
name: create-skill
description: >-
  Guides creation of Cursor Agent Skills for CPE (router/ONT) software testing
  teams. Use when authoring SKILL.md, adding skills under .cursor/skills/,
  naming cpe-* skills, or asking about skill structure in this repository.
disable-model-invocation: true
---

# Create Skill（CPE 测试团队）

在本仓库中创建或更新 Agent Skill。默认落盘路径：`.cursor/skills/<skill-name>/`。

## Phase 1：收集需求

向用户确认（可推断则不必逐项追问）：

| 项 | CPE 场景示例 |
|----|----------------|
| 目的 | 缺陷分诊、日志分析、TR-069/OMCI 检查、回归包、用例编写 |
| 范围 | 个人 `~/.cursor/skills/` 或本项目 `.cursor/skills/`（**默认本项目**） |
| 触发 | 用户说什么话时应加载（写入 `description`） |
| 输出 | 用例表、缺陷单、测试报告、检查清单 |
| 参考 | 现有用例库、缺陷模板、协议参数表 |

领域 Skill 命名：`cpe-<场景>`，小写连字符，≤64 字符。元技能不加 `cpe-` 前缀。

## Phase 2：设计

1. **description**（英文、第三人称）：写清 WHAT + WHEN，含触发词（如 GPON、TR-069、OMCI、PPPoE、Mesh、升级、拷机、syslog）。
2. **disable-model-invocation**：默认 `true`（显式 `@skill` 调用）；仅高频ambient任务（如日志分析）可省略。
3. **篇幅**：`SKILL.md` 正文 <500 行；细节放 `reference.md` / `examples.md`。
4. **自由度**：易出错流程用脚本或固定模板（低自由度）；评审类用检查清单（高自由度）。

## Phase 3：实现

目录结构：

```
.cursor/skills/<skill-name>/
├── SKILL.md          # 必需
├── reference.md      # 可选：协议/参数/日志关键字
├── examples.md       # 可选：输入输出样例
└── scripts/          # 可选：校验、解析
```

从模板复制：[templates/skill-skeleton/SKILL.md](templates/skill-skeleton/SKILL.md)

### SKILL.md 最小 frontmatter

```yaml
---
name: cpe-example
description: >-
  One-line WHAT. Use when user mentions triggers A, B, C.
disable-model-invocation: true
---
```

### CPE 正文建议章节

- **Prerequisites**：固件版本、组网拓扑、账号类型（勿写真实密码）
- **Workflow**：分步清单，可勾选
- **Output template**：缺陷单 / 用例 / 报告固定 Markdown
- **Log capture**：必抓日志列表与命令占位
- **Additional resources**：链到 `reference.md`（仅一层）

## Phase 4：验收

- [ ] `description` 含触发词，第三人称英文
- [ ] 无真实密钥、SN、内网 IP
- [ ] 术语统一（DUT、CPE、ONT、Router、WAN/LAN）
- [ ] 引用文件仅一层深度
- [ ] 已更新 `README.md` 技能列表（若团队维护目录表）

## 反模式

- 勿写入 `~/.cursor/skills-cursor/`
- 勿在 Skill 里堆通用编程教程
- 勿混用「光猫 / ONT / SFU」指代而不定义

## 资源

- 官方完整指南：Cursor 内置 `create-skill`（`~/.cursor/skills-cursor/create-skill/`）
- 骨架模板：[templates/skill-skeleton/](templates/skill-skeleton/)
