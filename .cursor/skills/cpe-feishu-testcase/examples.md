# 飞书用例示例（脱敏）

## 示例 1：WAN PPPoE（通用）

```markdown
## 用例

### 1. 关联项目
TBD_FEISHU_PROJECT

### 2. 用例名称/标题
【EVO6022GP3】【LLA】【WAN】PPPoE 首次拨号成功_实网上联；

### 3. 用例类型
功能测试

### 4. 用例分级
P0

### 5. 标签
LLA,WAN

### 6. 前置条件
- DUT：EVO6022GP3，软件版本 TBD（测试环境）
- 初始状态：恢复出厂；Internet WAN 默认 PPPoE
- 拓扑：GPON 上联；LAN1 下挂 PC1
- 测试数据：`TEST_PPPOE_USER` / `TEST_PPPOE_PASS`（测试环境专用）

### 7. 测试步骤
1. 登录 Web WAN 页，确认当前为 PPPoE。
2. 填入测试账号并应用。
3. PC1 ping 外网检测地址 `203.0.113.1`。

### 8. 预期结果
1. 页面显示 PPPoE，无配置错误。
2. WAN Connected，获 IPv4。
3. ping 10 次无丢包。
```

## 示例 2：标题 ❌ / ✅

| | 标题 |
|---|------|
| ❌ | ACS 改 WAN |
| ❌ | 【LLA】改拨号 |
| ✅ | 【EVO6022GP3】【LLA】【ACS】支持通过acs节点，将internet wan由默认pppoe拨号方式修改成ipoe，也支持修改回pppoe； |
| ✅ | 【EVO6022GP3】【LLA】【ACS】通过ACS节点将Internet WAN由默认PPPoE修改为IPoE； |

## 示例 3：EVO6022GP3 ACS WAN PPPoE ↔ IPoE

基于团队标题的**可执行** 8 字段示例（节点路径为占位，导入飞书前替换为正式 TR-069 路径）。

```markdown
## 用例

### 1. 关联项目
TBD_FEISHU_PROJECT

### 2. 用例名称/标题
【EVO6022GP3】【LLA】【ACS】支持通过acs节点，将internet wan由默认pppoe拨号方式修改成ipoe，也支持修改回pppoe；

### 3. 用例类型
功能测试

### 4. 用例分级
P0

### 5. 标签
LLA,ACS

### 6. 前置条件
- DUT：EVO6022GP3，软件版本 TBD（测试环境）
- 初始状态：恢复出厂默认配置；**Internet WAN 默认 PPPoE**，且 PPPoE 拨号成功、可上网
- 拓扑：GPON 上联实网或仿真；LAN1 下挂 PC1
- ACS：设备已在 `ACS_URL` 上线，Inform 正常；已备数据模型中 Internet WAN 相关节点表
- 测试数据：`TEST_PPPOE_USER` / `TEST_PPPOE_PASS`（测试环境专用）

### 7. 测试步骤

**阶段一：PPPoE → IPoE**

1. 在 ACS 上对 Internet WAN 执行 Get，记录当前连接类型/拨号方式为 PPPoE（节点 `TBD_NODE_WAN_TYPE`）。
2. 通过 ACS Set 将 Internet WAN 拨号方式改为 **IPoE**（写入 `TBD_NODE_WAN_TYPE` 及 IPoE 所需参数，以数据模型为准）。
3. 等待设备应用配置（建议 ≤120s），直至 ACS/Get 或 Web WAN 页显示 IPoE 且 WAN 为 Connected。
4. PC1 访问外网（ping `203.0.113.1` 或 HTTP 探测）。

**阶段二：IPoE → PPPoE**

5. 通过 ACS Set 将 Internet WAN 拨号方式改回 **PPPoE**，填入 `TEST_PPPOE_USER` / `TEST_PPPOE_PASS`。
6. 等待 PPPoE 拨号成功（WAN Connected，获 IPv4）。
7. PC1 再次访问外网；ACS Get 核对节点与 Web 显示均为 PPPoE。

### 8. 预期结果

**阶段一**

1. Get 值为 PPPoE，与 Web 一致。
2. Set 成功，无 ACS 故障码；设备无异常重启。
3. WAN 为 IPoE 且 Connected；获有效 IP（DHCP/静态依模型）。
4. PC1 外网访问成功。

**阶段二**

5. Set 成功，PPPoE 账号生效。
6. PPPoE 拨号成功，日志无持续认证失败。
7. PC1 外网访问成功；Get/Web 均为 PPPoE，与阶段一前基线一致。
```

### 示例 3b：拆分写法（推荐执行跟踪）

同需求拆为两条时，标题与步骤仅保留单方向，分级/标签不变。第二条标题：

```text
【EVO6022GP3】【LLA】【ACS】通过ACS节点将Internet WAN由IPoE修改回PPPoE；
```

前置中初始状态第二条改为：**当前 Internet WAN 已为 IPoE 且可上网**。

## 示例 4：批量生成 10 条 P0 WIFI

### 用户怎么说（复制即用）

```text
@cpe-feishu-testcase 请生成 10 条 P0 级别 WIFI 功能模块测试用例：

【产品】EVO6022GP3，软件版本 Vx.x.x_TBD
【关联项目】TBD_FEISHU_PROJECT
【项目标签】LLA
【类型】功能测试
【WAN】已 PPPoE 拨号上网
【WiFi 默认】双频开启，SSID/密码用占位符
【范围】仅输出 test-strategy §4.2 WIFI 中判定为 P0 的用例（不足 10 条则说明）
【输出】先测试点矩阵，再 10 条完整 8 字段，用 --- 分隔
【保存】testcases/evo6022gp3/wifi/batch-p0-10.md
```

### Agent 应交付的结构（节选）

```markdown
# 用例集：EVO6022GP3 / WIFI / 目标P0 / 实际P0:6

## 分级统计
| 级别 | 条数 |
|------|------|
| P0 | 6 |
| P1 | 4 |

说明：按 SR7D4VA 测试策略，基本功能为 P0，访客/隐藏 SSID 等为 P1，不凑 P0。

## 测试点矩阵
| 序号 | 标题摘要 | 分级 | 分级依据 | 标签 |
|------|----------|------|----------|------|
| 1 | 2.4G 基本功能/关联 | P0 | P0 \| 策略:WEB-WIFI-基本功能 \| SR7D4VA§4.2 | LLA,WIFI |
| 6 | 访客 WiFi | P1 | P1 \| 策略:WEB-WIFI-扩展 \| 访客wifi | LLA,WIFI |

---

## 用例 1
### 1. 关联项目
TBD_FEISHU_PROJECT
### 2. 用例名称/标题
【EVO6022GP3】【LLA】【WIFI】2.4G 频段默认 SSID 与密码关联成功；
…（字段 3–8 完整）
```

### 自定义 10 条时

若不要默认池，在提示词中列出 10 个测试点：

```text
测试点列表：
1. …
2. …
…
10. …
```

## 示例 5：国际自动分级 10 条 WIFI

```text
@cpe-feishu-testcase 生成 10 条 WIFI 功能用例：
- 型号 EVO6022GP3，产品类型：光猫（运营商）
- 按 test-strategy.md（SR7D4VA 测试策略）自动判级
- 输出分级统计 + 矩阵（含分级依据）+ 完整 8 字段
```

预期：P0 约 5–6 条（2.4G/5G 默认、双频合一、WPA2、WiFi 上网）；P1 约 4–5 条（隐藏 SSID、WiFi Web、改密、重启）。

## 示例 6：ACS 用例定级（Mandatory P0）

标题：

```text
【EVO6022GP3】【LLA】【ACS】支持通过acs节点，将internet wan由默认pppoe拨号方式修改成ipoe，也支持修改回pppoe；
```

字段 4 与依据：

```markdown
### 4. 用例分级
P0

> 分级依据：P0 | 策略:TR069-ACS-WAN | SR7D4VA§4.4 | ACS WAN PPPoE↔IPoE
```
