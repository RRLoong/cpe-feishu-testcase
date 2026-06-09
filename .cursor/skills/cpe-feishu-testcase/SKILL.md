---
name: cpe-feishu-testcase
description: >-
  Feishu 8-field CPE test cases; auto-grades P0-P3 per test-strategy.md (SR7D4VA).
  Use for 飞书用例、用例分级、P0-P3、测试策略、批量生成、WIFI、TR069、ACS.
disable-model-invocation: true
---

# cpe-feishu-testcase

路由器/光猫测试用例 → **飞书 8 字段** + **P0–P3 自动分级**。

## 文档（按需阅读）

| 文档 | 内容 |
|------|------|
| [reference.md](reference.md) | 8 字段定义、标题格式、步骤/预期写法 |
| [test-strategy.md](test-strategy.md) | P0–P3、模块矩阵、判级流程 |
| [examples.md](examples.md) | 提示词与输出样例 |

## 何时执行

| 用户意图 | 动作 |
|----------|------|
| 含「生成/编写/完善用例」 | 输出完整 8 字段 |
| 仅「评审/检查格式/判级」 | 对照 reference + test-strategy，不生成 |

## 生成流程

1. 读 [reference.md](reference.md) 填 8 字段。
2. 读 [test-strategy.md](test-strategy.md) §2 判级 + §4 矩阵定 P0–P3，写**分级依据**。
3. 缺关联项目/型号/版本 → `TBD` 或追问。
4. 批量 ≥3 条：先**分级统计** + **测试点矩阵**，再逐条用例（`---` 分隔）。
5. 用户要求保存 → `testcases/<型号小写>/<模块>/`。

### 批量要点

- **仅 P0**：只取 test-strategy §4 对应模块 **P0 列**；不足 N 条须说明，**禁止凑 P0**（如隐藏 SSID、访客 WiFi 为 P1）。
- **未指定分级**：按矩阵混合 P0/P1/P2。

### 用户指令速查

见 [test-strategy.md §2.1](test-strategy.md#21-与用户指令)。

## 输出模板

字段名不得改：

```markdown
## 用例

### 1. 关联项目
### 2. 用例名称/标题
【<型号>】【<项目>】【<模块>】<功能描述>；

### 3. 用例类型
功能测试

### 4. 用例分级
P0

> 分级依据：P0 | 策略:WEB-WIFI-基本功能 | SR7D4VA§4.2

### 5. 标签
LLA,WIFI

### 6. 前置条件
### 7. 测试步骤
### 8. 预期结果
```

## 安全

占位符：`TEST_PPPOE_USER`、`ACS_URL`、`TBD_NODE_*`；禁止真实密码与 SN。

## 示例

[examples.md](examples.md)
