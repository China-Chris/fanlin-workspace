# OpenClaw 零基础安装指南

> 从零开始，在 10 分钟内拥有自己的 AI 助理

---

## 什么是 OpenClaw？

OpenClaw 是一个**本地运行的 AI 助理平台**。它可以：
- 连接你常用的通讯工具（微信、Telegram、WhatsApp、Slack、Discord 等）
- 执行代码、控制浏览器、管理文件
- 定时任务、自动化工作流
- 语音交互（macOS/iOS/Android）

**核心特点**：数据本地、隐私优先、完全可控。

---

## 前置条件

| 项目 | 要求 |
|------|------|
| 操作系统 | macOS / Linux / Windows (WSL2) |
| Node.js | ≥ 22 |
| 网络 | 需要访问 GitHub 和 npm |
| 内存 | 建议 8GB+ |

---

## 第一步：配置免费 VPN（国内用户必看）

由于 OpenClaw 需要从 GitHub/npm 下载，国内用户需要先配置网络。

### 推荐免费方案

#### 方案 A：Watt Toolkit（Steam++）- 最简单
```bash
# 1. 下载 Watt Toolkit
# 官网：https://steampp.net/
# 选择对应系统版本下载安装

# 2. 打开软件，勾选以下加速项：
#    ✅ GitHub
#    ✅ npm
#    ✅ Docker Hub（可选）

# 3. 点击「一键加速」
```

#### 方案 B：手动 Hosts 修改
```bash
# 使用 GitHub 加速服务修改 hosts
# 工具推荐：SwitchHosts（跨平台）

# 1. 下载 SwitchHosts
# https://github.com/oldj/SwitchHosts/releases

# 2. 添加远程 hosts 源：
# URL: https://raw.githubusercontent.com/ineo6/hosts/master/hosts
# 自动更新：每 1 小时

# 3. 启用后刷新 DNS
echo "Hosts 已更新"
```

#### 方案 C：npm 镜像（仅解决 npm 问题）
```bash
# 临时使用淘宝镜像
npm config set registry https://registry.npmmirror.com

# 或者使用 nrm 管理
npm install -g nrm
nrm use taobao

# 安装完 OpenClaw 后恢复
npm config set registry https://registry.npmjs.org
```

### 验证网络
```bash
# 测试 GitHub 连通性
ping github.com

# 测试 npm
npm ping
```

---

## 第二步：安装 Node.js

```bash
# 使用 nvm 安装（推荐）
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash

# 重新加载 shell
source ~/.bashrc  # Linux
source ~/.zshrc   # macOS

# 安装 Node.js 22
nvm install 22
nvm use 22

# 验证
node --version  # v22.x.x
npm --version   # 10.x.x
```

**Windows 用户**：直接下载安装包 https://nodejs.org/dist/v22.0.0/

---

## 第三步：安装 OpenClaw

```bash
# 全局安装 OpenClaw
npm install -g openclaw@latest

# 或者使用 pnpm（更快）
pnpm add -g openclaw@latest

# 验证安装
openclaw --version
```

---

## 第四步：运行配置向导

```bash
# 启动交互式配置向导
openclaw onboard --install-daemon
```

向导会引导你完成：
1. **工作目录**设置（默认 `~/.openclaw`）
2. **模型配置**（OpenAI / Anthropic / 其他）
3. **通讯渠道**（Telegram Bot / WhatsApp 等）
4. **守护进程**安装（自动启动）

### 模型配置示例
```bash
# 选择模型提供商
? 选择模型: OpenAI
? API Key: sk-xxxxxxxxxx
? 默认模型: gpt-4o

# 或者 Anthropic（推荐长文本场景）
? 选择模型: Anthropic
? API Key: sk-ant-xxxxxxxxxx
? 默认模型: claude-opus-4-6
```

### Telegram 配置（最简单入门）
```bash
? 启用 Telegram: Yes
? Bot Token: 从 @BotFather 获取
? 允许的用户: 你的 Telegram 数字 ID
```

获取 Bot Token：
1. 在 Telegram 搜索 @BotFather
2. 发送 `/newbot`
3. 按提示创建，保存 Token

---

## 第五步：启动 Gateway

```bash
# 手动启动（调试模式）
openclaw gateway --verbose

# 或者使用守护进程（已安装的话）
openclaw gateway start

# 查看状态
openclaw gateway status
```

默认地址：`ws://127.0.0.1:18789`

---

## 第六步：发送第一条消息

```bash
# 命令行测试
openclaw agent --message "你好，OpenClaw！"

# 或者发送给已配置的渠道
openclaw message send --to "你的手机号/WhatsApp账号" --message "Hello"
```

---

## 常见问题

### Q: 安装时报错 `ECONNREFUSED`
**原因**：网络不通，无法下载依赖  
**解决**：检查 VPN/加速器是否开启，参考第一步

### Q: `node: --version` 显示版本不对
**原因**：Node.js 版本过低  
**解决**：升级到 22+，`nvm install 22`

### Q: 提示权限不足
```bash
# macOS/Linux 权限修复
sudo chown -R $(whoami) ~/.npm
sudo chown -R $(whoami) ~/.openclaw
```

### Q: Windows 能用吗？
能用，但**强烈推荐使用 WSL2**：
```powershell
# 在 WSL2 Ubuntu 中安装
wsl --install -d Ubuntu
# 然后在 Ubuntu 中按本教程操作
```

### Q: 没有境外 API Key 怎么办？
- OpenAI：需要海外信用卡
- Anthropic：同样需要
- **替代方案**：使用 OpenRouter（国内可用）、Kimi（国内）、或其他国内兼容 API

---

## 下一步

安装完成后，你可以：

1. **配置更多渠道**：WhatsApp、Slack、Discord、微信（BlueBubbles）
2. **安装 Skills**：`openclaw skills search`
3. **设置定时任务**：`openclaw cron add`
4. **浏览器自动化**：安装 Chrome 扩展

查看完整文档：https://docs.openclaw.ai

---

## 快捷命令参考

| 命令 | 作用 |
|------|------|
| `openclaw onboard` | 配置向导 |
| `openclaw gateway status` | 查看状态 |
| `openclaw gateway start/stop/restart` | 控制服务 |
| `openclaw doctor` | 诊断问题 |
| `openclaw agent -m "xxx"` | 发送消息给 AI |
| `openclaw configure` | 修改配置 |

---

有问题？加入 Discord 社区：https://discord.gg/clawd 🦞
