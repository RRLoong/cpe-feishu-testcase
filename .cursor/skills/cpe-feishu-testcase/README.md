# cpe-feishu-testcase

CPE 飞书用例 Skill：**P0–P3 自动判级** + **飞书导入 CSV/XLSX**（20 列模板，已移除废弃列）。

## 快速使用

1. Cursor 打开含本 Skill 的工作区
2. `@cpe-feishu-testcase` + 需求（须含「生成/编写」）

```text
@cpe-feishu-testcase 生成 10 条 WIFI 用例，型号 SR7D4VA，项目标签 LLA，自动判级，飞书导入 CSV
```

**默认输出**：分级统计 → 测试点矩阵 → **飞书导入 CSV**（非 Markdown 分段）。  
需要 Markdown 8 字段时加：`Markdown 分段输出`。

## 导入飞书

| 步骤 | 操作 |
|------|------|
| 1 | Agent 生成 CSV（表头见 [feishu-import-template.xlsx](feishu-import-template.xlsx)） |
| 2 | 存为 `.csv`（UTF-8 BOM）或粘贴进模板另存 `.xlsx` |
| 3 | 飞书项目 → 用例 → **导入** |
| 4 | **先导入 1 条**验证「步骤 / 预期结果」 |

### 固定约定

| 项 | 规则 |
|----|------|
| 所属目录 | 固定 `CPE` |
| 用例类型 | 仅 `功能测试` / `兼容性测试`（默认功能测试） |
| 用例分级 | `P0`–`P3`（见 [test-strategy.md](test-strategy.md)） |
| 步骤 / 预期 | CSV 的 **步骤**、**预期结果** 列 |
| 分级依据 | CSV 的 **描述** 列 |

列映射详见 [reference.md §9](reference.md#9-飞书导入列映射)。

## 常用提示词

```text
# 批量 + 自动判级 + 飞书 CSV
@cpe-feishu-testcase 生成 10 条 WIFI 用例，型号 SR7D4VA，自动判级，飞书导入 CSV

# 仅 P0
@cpe-feishu-testcase 生成 10 条 P0 WIFI 用例，型号 SR7D4VA，飞书导入 CSV

# 指定关联项目
@cpe-feishu-testcase 生成 5 条 ACS 用例，型号 SR7D4VA，关联项目 xxx研发项目，飞书导入 CSV
```

更多见 [examples.md](examples.md)。

## 文档

| 文件 | 用途 |
|------|------|
| [SKILL.md](SKILL.md) | Agent 流程 |
| [reference.md](reference.md) | 8 字段 + 飞书 20 列映射 |
| [test-strategy.md](test-strategy.md) | P0–P3 与模块矩阵 |
| [examples.md](examples.md) | 提示词与 CSV 样例 |
| [feishu-import-template.xlsx](feishu-import-template.xlsx) | 飞书导入表头（20 列，无废弃字段） |

## 说明

- 必须 `@cpe-feishu-testcase`（不会自动加载）
- 判级默认按 SR7D4VA 测试策略（[test-strategy.md](test-strategy.md) §4）
- 勿提交真实密码、SN、内网 IP；使用占位符
