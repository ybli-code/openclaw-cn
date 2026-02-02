# OpenClaw (原 Clawdbot) 中文入门指南
---
OpenClaw 是一款强大的开源个人 AI 助手，由 Peter Steinberger 开发。它不仅能回答问题，还能主动执行任务，如操作系统、访问网页、处理邮件、自动编写代码等。

**本项目目的：**
长期维护 OpenClaw 的汉化与中文 Skills 的接入，为中文用户提供更好的使用体验。

## 1. 项目背景与演进

OpenClaw 的项目名称经历了几次演变：
- **Clawdbot / Clawbot**: 最初的项目名，灵感来自 Claude 和龙虾爪 (claw)。
- **Moltbot**: 2026 年 1 月 27 日，因版权顾虑临时更名为 Moltbot（意为脱壳的龙虾）。
- **OpenClaw**: 2026 年 1 月 30 日确定的最终官方名称，强调开源性和长线品牌。

## 2. 安装方法

### 2.1 推荐方式：一键脚本
这是最简单的方式，会自动安装 Node.js (≥22) 并完成基本配置。

- **macOS / Linux**:
  ```bash
  curl -fsSL https://openclaw.ai/install.sh | bash
  ```
- **Windows (PowerShell)**:
  ```powershell
  iwr -useb https://openclaw.ai/install.ps1 | iex
  ```

### 2.2 手动安装
需要预先安装 **Node.js ≥22**。

- **使用 npm**:
  ```bash
  npm install -g openclaw@latest
  ```
- **使用 pnpm**:
  ```bash
  pnpm add -g openclaw@latest
  ```

安装完成后，运行入职向导：
```bash
openclaw onboard --install-daemon
```

### 2.3 源码安装 (开发模式)
```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
pnpm install
pnpm ui:build   # 构建前端界面
pnpm build      # 构建整个项目
pnpm openclaw onboard --install-daemon
```

## 3. 配置流程

运行 `openclaw onboard` 后，按照以下步骤操作：
1. **QuickStart**: 选择快速启动。
2. **AI Provider**: 配置模型供应商。支持 Anthropic (推荐 Claude 3.5/4.5), OpenAI, 以及国内的 Qwen (通义千问), MiniMax, 智谱 AI 等。
3. **Channels**: 选择聊天工具。支持 WhatsApp, Telegram, Slack, Discord, Signal, iMessage 等。
4. **Skills**: 选择并启用技能（如搜索、浏览器控制、文件处理等）。
5. **完成**: 配置文件将保存在 `~/.openclaw/openclaw.json`。

## 4. 常用命令

- `openclaw status`: 查看当前运行状态。
- `openclaw gateway start`: 启动网关服务。
- `openclaw gateway stop`: 停止网关服务。
- `openclaw doctor`: 诊断配置问题或进行版本迁移。
- `openclaw message send --to <target> --message <text>`: 发送消息。

## 5. 访问界面

网关启动后，默认可以通过浏览器访问：`http://127.0.0.1:18789/chat`。

---

## 文档链接

- [English README (英文官方文档)](file:///Users/ybli/Documents/Projects/openclaw-cn/README-EN.md)
- [Chinese README (中文翻译文档)](file:///Users/ybli/Documents/Projects/openclaw-cn/README-CN)

