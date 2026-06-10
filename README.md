# CPE Cursor Skills

路由器 / 光猫（CPE）测试团队的 Cursor Skills 与 Rules。

## 快速使用

1. Cursor **Open Folder** 打开本仓库
2. 对话：`@cpe-feishu-testcase` + 需求（生成须含「生成/编写」）

```text
@cpe-feishu-testcase 生成 10 条 WIFI 用例，型号 SR7D4VA，自动判级
```

主 Skill 路径：`.cursor/skills/cpe-feishu-testcase/`（详见该目录 [README.md](.cursor/skills/cpe-feishu-testcase/README.md)）

## 分发给同事

| 方式 | 操作 |
|------|------|
| **GitHub（推荐）** | Clone 本仓库 → Cursor 打开 clone 目录 |
| **Zip** | 解压得 `skills` 文件夹 → Cursor 打开；删 `__MACOSX`（若有） |
| **嵌入测试项目** | 复制 `.cursor/skills/cpe-feishu-testcase/` 到 `项目/.cursor/skills/` |
| **全局可用** | 复制到 `~/.cursor/skills/cpe-feishu-testcase/`（任意项目可 `@`） |

打包勿含：`.git/`、`.venv_numbers/`、`*.zip`。

## 仓库结构

```text
.cursor/skills/     # Agent Skills（含 cpe-feishu-testcase）
.cursor/rules/      # 团队 Rules（命名、安全等约束）
```

## 安全

勿提交真实密码、SN、内网 IP；使用 `DUT_SN`、`WAN_IP` 等占位符。
