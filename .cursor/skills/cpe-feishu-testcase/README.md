# cpe-feishu-testcase

飞书 **8 字段** CPE 测试用例 + **测试策略** 自动 **P0–P3** 分级。

## 使用

1. Cursor 打开本 **skills** 仓库（或已将本 Skill 复制到项目 `.cursor/skills/`）。
2. 对话中 `**@cpe-feishu-testcase`** + 自然语言需求。

### 固定要求


| 要求                        | 说明                           |
| ------------------------- | ---------------------------- |
| 必须 `@cpe-feishu-testcase` | 本 Skill 不会自动加载，须手动 @         |
| 生成完整用例                    | 须含 **生成 / 编写 / 完善用例** 等动词    |
| 仅评审不生成                    | 说 **评审 / 检查格式 / 判级**，可粘贴已有用例 |


### 快速示例

```text
@cpe-feishu-testcase 生成 10 条 WIFI 功能用例，型号 SR7D4VA，自动判级
```

### 多种用法

**批量 + 自动判级（P0–P3 混合）**

```text
@cpe-feishu-testcase 生成 10 条 WIFI 功能用例，型号 SR7D4VA，项目标签 LLA，按测试策略自动判级
```

**只要 P0（不凑数）**

```text
@cpe-feishu-testcase 生成 10 条 P0 级别 WIFI 用例，型号 SR7D4VA
```

策略矩阵里 P0 不足 10 条时会说明；隐藏 SSID、访客 WiFi 等为 P1，不会硬标 P0。

**单条 / 指定模块**

```text
@cpe-feishu-testcase 编写 1 条 ACS 用例：Internet WAN 从 PPPoE 改 IPoE 再改回，型号 EVO6022GP3，标签 LLA
```

**你指定测试点列表**

```text
@cpe-feishu-testcase 按下面测试点生成用例，型号 SR7D4VA，自动判级：
1. 2.4G 默认 SSID 关联
2. 5G 默认 SSID 关联
3. …
```

**结构化长提示（批量交付推荐）**

```text
@cpe-feishu-testcase 请生成 10 条 P0 级别 WIFI 功能模块测试用例：

【产品】SR7D4VA，软件版本 Vx.x.x_TBD
【关联项目】TBD_FEISHU_PROJECT
【项目标签】LLA
【WAN】已 PPPoE 拨号上网
【范围】仅 test-strategy §4.2 WIFI 中判定为 P0 的用例
【输出】先分级统计 + 测试点矩阵，再完整 8 字段，用 --- 分隔
【保存】testcases/sr7d4va/wifi/batch-p0-10.md
```

**评审 / 判级（不生成新用例）**

```text
@cpe-feishu-testcase 检查下面用例的 8 字段格式和 P0–P3 是否合理：

（粘贴用例正文）
```

**完善已有草稿**

```text
@cpe-feishu-testcase 完善下面用例：补全前置条件、步骤、预期，并按 SR7D4VA 策略判级：

（粘贴草稿）
```

### 说法与 Agent 行为


| 你怎么说                  | Agent 怎么做                                                   |
| --------------------- | ----------------------------------------------------------- |
| 未写分级 / 「自动判级」         | 按 [test-strategy.md](test-strategy.md) P0–P3 混合，先出分级统计 + 矩阵 |
| 「按测试策略」「SR7D4VA 策略」   | 严格按 test-strategy.md                                        |
| 「生成 N 条 P0 + 模块名」     | 仅 §4 该模块 **P0 列**；不足 N 条须说明                                 |
| 「生成 N 条 + 模块名」（未写 P0） | P0–P3 混合 + 分级统计                                             |
| 「全部 P0」               | 字段 4 可标 P0，分级依据保留建议级并注「用户覆盖」                                |
| 批量 ≥3 条               | 先矩阵再逐条 8 字段                                                 |
| 要求「保存」                | 写入 `testcases/<型号小写>/<模块>/`                                 |


更多可复制提示词见 [examples.md](examples.md)（含 ACS、国际兜底、拆分写法等）。

## 文档结构（5 个文件）

```
cpe-feishu-testcase/
├── README.md           ← 本文件（给人看）
├── SKILL.md            ← Agent 入口（流程）
├── reference.md        ← 飞书 8 字段
├── test-strategy.md    ← P0–P3 + 模块矩阵 + 判级
└── examples.md         ← 提示词样例
```


| 你想…        | 打开                                   |
| ---------- | ------------------------------------ |
| 字段怎么填      | [reference.md](reference.md)         |
| 为什么是 P0/P1 | [test-strategy.md](test-strategy.md) |
| 复制提示词      | [examples.md](examples.md)           |


## 策略原件（团队维护，仓库外）

`SR7D4VA_0.0.0.1版本_测试策略.md`

更新后请同步 [test-strategy.md](test-strategy.md) §4 矩阵。

## 安全

勿提交真实密码、SN、客户专网 IP；使用测试环境占位符。