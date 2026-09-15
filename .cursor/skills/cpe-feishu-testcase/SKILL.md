---
name: cpe-feishu-testcase
description: >-
  Feishu CPE test cases with CSV/XLSX import format; auto-grades P0-P3 per test-strategy.md.
  Use for 飞书用例、用例导入、CSV、xlsx、用例分级、P0-P3、批量生成、WIFI、ACS.
disable-model-invocation: true
---

# cpe-feishu-testcase

路由器/光猫测试用例 → **飞书导入 CSV** + **P0–P3 自动分级**。

## 文档（按需阅读）

| 文档 | 内容 |
|------|------|
| [reference.md](reference.md) | 8 字段、飞书 20 列映射、步骤/预期写法（含标题格式 §2） |
| [cpe-mf-tree.md](cpe-mf-tree.md) | CPE 用例目录 M/F 树（标题占号） |
| [test-strategy.md](test-strategy.md) | P0–P3、模块矩阵、判级流程（判级唯一依据） |
| [Router_Pon_测试范围模版.md](Router_Pon_测试范围模版.md) | 测试范围模版（Numbers 同步源；非运行时判级入口） |
| [examples.md](examples.md) | 提示词与 CSV 样例 |
| [feishu-import-template.xlsx](feishu-import-template.xlsx) | 飞书导入表头（20 列，已移除废弃列） |

## 何时执行

| 用户意图 | 动作 |
|----------|------|
| 含「生成/编写/完善用例」 | 输出飞书导入 CSV（默认） |
| 含「Markdown / 分段 / 8 字段」 | 输出 § 内 Markdown 8 字段模板 |
| 仅「评审/检查格式/判级」 | 对照 reference + test-strategy，不生成 |

## 生成流程

1. 读 [reference.md](reference.md) 填 8 字段语义内容。
2. **判级只读** [test-strategy.md](test-strategy.md)：**§1 正式约束**（定义/判定要点/失败后果/执行要求）+ §2 流程 + §4 矩阵定 P0–P3；**分级依据**写入 CSV **描述**列。  
   - [Router_Pon_测试范围模版.md](Router_Pon_测试范围模版.md) / `.numbers` 仅为策略同步源；**不要**跨仓库查找外部策略文件。
3. 缺关联项目/型号/版本 → `TBD_FEISHU_PROJECT` / `TBD` 或追问。
4. 批量 ≥3 条：先**分级统计** + **测试点矩阵**，再交付 **CSV 导入表**。
5. 用户要求保存 → `testcases/<型号小写>/<模块>/feishu-import-<批次>.csv`（UTF-8 BOM）。

### 飞书 CSV 规则（默认输出）

- 表头与 [feishu-import-template.xlsx](feishu-import-template.xlsx) **完全一致**（20 列，顺序不变）。
- 模板已移除废弃列：**执行步骤**、**[废弃]预期结果**（勿再输出这两列）。
- **所属目录**固定填 `CPE`。
- **用例类型**仅 `功能测试` 或 `兼容性测试`（未说明默认 `功能测试`；OLT/终端/光模块等兼容性场景用 `兼容性测试`）。
- 8 字段内容映射见 [reference.md §9](reference.md#9-飞书导入列映射)。
- **步骤** / **预期结果**列：单元格内编号列表 `1.` `2.`…。
- 其余未映射列留空。
- CSV：UTF-8 **带 BOM**；含换行/逗号的单元格用双引号包裹。

### 批量要点

- **仅 P0**：只取 test-strategy §4 对应模块 **P0 列**；不足 N 条须说明，**禁止凑 P0**。
- **未指定分级**：按矩阵混合 P0/P1/P2。

### 用户指令速查

见 [test-strategy.md §2.1](test-strategy.md#21-与用户指令)。

## Markdown 8 字段模板（仅用户明确要求时）

```markdown
### 1. 关联项目
### 2. 用例名称/标题
【Mxxx-Fxxx-Cxxx】【<模块标签>】【<客户定制型号?>】【P0|P1|P2|P3】【auto|manual】<功能描述>

### 3. 用例类型
功能测试

### 4. 用例分级
P0

### 5. 标签
LLA,WIFI

### 6. 前置条件
### 7. 测试步骤
### 8. 预期结果
```

标题段含义与占号规则见 [reference.md §2](reference.md#2-用例名称标题)；`M`/`F` 目录见 [cpe-mf-tree.md](cpe-mf-tree.md)。  
**【客户定制型号】** 可选：未指定型号则整段省略。

## 安全

占位符：`TEST_PPPOE_USER`、`ACS_URL`、`TBD_NODE_*`；禁止真实密码与 SN。

## 示例

[examples.md](examples.md)
