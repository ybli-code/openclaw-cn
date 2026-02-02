# 🦞 OpenClaw — 个人 AI 助手

<p align="center">
    <picture>
        <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text-dark.png">
        <img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text.png" alt="OpenClaw" width="500">
    </picture>
</p>

<p align="center">
  <strong>EXFOLIATE! EXFOLIATE!</strong>
</p>

<p align="center">
  <a href="https://github.com/openclaw/openclaw/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/openclaw/openclaw/ci.yml?branch=main&style=for-the-badge" alt="CI status"></a>
  <a href="https://github.com/openclaw/openclaw/releases"><img src="https://img.shields.io/github/v/release/openclaw/openclaw?include_prereleases&style=for-the-badge" alt="GitHub release"></a>
  <a href="https://discord.gg/clawd"><img src="https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge" alt="Discord"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
</p>

**OpenClaw** 是一款运行在您自己设备上的 *个人 AI 助手*。
它在您已有的渠道上为您提供服务（WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, WebChat），并支持 BlueBubbles, Matrix, Zalo 和 Zalo Personal 等扩展渠道。它可以在 macOS/iOS/Android 上进行语音交流，并能渲染一个由您控制的实时 Canvas（画布）。Gateway（网关）只是控制平面 —— 产品本身就是这个助手。

如果您想要一个私密的、单用户的、感觉像是在本地运行、响应迅速且始终在线的助手，那么这就是您的选择。

[网站](https://openclaw.ai) · [文档](https://docs.openclaw.ai) · [DeepWiki](https://deepwiki.com/openclaw/openclaw) · [入门指南](https://docs.openclaw.ai/start/getting-started) · [更新](https://docs.openclaw.ai/install/updating) · [展示](https://docs.openclaw.ai/start/showcase) · [常见问题](https://docs.openclaw.ai/start/faq) · [向导](https://docs.openclaw.ai/start/wizard) · [Nix](https://github.com/openclaw/nix-clawdbot) · [Docker](https://docs.openclaw.ai/install/docker) · [Discord](https://discord.gg/clawd)

推荐设置：运行入职向导 (`openclaw onboard`)。它会引导您完成网关、工作区、渠道和技能的配置。CLI 向导是推荐路径，适用于 **macOS、Linux 和 Windows (通过 WSL2；强烈推荐)**。
支持 npm, pnpm 或 bun。
新安装？从这里开始：[入门指南](https://docs.openclaw.ai/start/getting-started)

**订阅 (OAuth):**

- **[Anthropic](https://www.anthropic.com/)** (Claude Pro/Max)
- **[OpenAI](https://openai.com/)** (ChatGPT/Codex)

模型说明：虽然支持任何模型，但我强烈建议使用 **Anthropic Pro/Max (100/200) + Opus 4.5**，因为它具有更强的长上下文处理能力和更好的提示词注入防御能力。请参阅 [入职配置](https://docs.openclaw.ai/start/onboarding)。

## 模型 (选择 + 认证)

- 模型配置 + CLI: [Models](https://docs.openclaw.ai/concepts/models)
- 认证配置轮换 (OAuth vs API 密钥) + 备用方案: [Model failover](https://docs.openclaw.ai/concepts/model-failover)

## 安装 (推荐)

运行环境: **Node ≥22**。

```bash
npm install -g openclaw@latest
# 或: pnpm add -g openclaw@latest

openclaw onboard --install-daemon
```

向导会安装 Gateway 守护进程 (launchd/systemd 用户服务) 以保持持续运行。

## 快速开始 (简要版)

运行环境: **Node ≥22**。

完整的新手指南 (认证、配对、渠道): [Getting started](https://docs.openclaw.ai/start/getting-started)

```bash
openclaw onboard --install-daemon

openclaw gateway --port 18789 --verbose

# 发送消息
openclaw message send --to +1234567890 --message "Hello from OpenClaw"

# 与助手对话 (可选地发送回任何已连接的渠道: WhatsApp/Telegram/Slack/Discord/Google Chat/Signal/iMessage/BlueBubbles/Microsoft Teams/Matrix/Zalo/Zalo Personal/WebChat)
openclaw agent --message "Ship checklist" --thinking high
```

正在升级？请参阅 [更新指南](https://docs.openclaw.ai/install/updating) (并运行 `openclaw doctor`)。

## 开发渠道

- **stable**: 标记版本 (`vYYYY.M.D` 或 `vYYYY.M.D-<patch>`), npm dist-tag 为 `latest`。
- **beta**: 预发布标记 (`vYYYY.M.D-beta.N`), npm dist-tag 为 `beta` (可能缺少 macOS 应用)。
- **dev**: `main` 分支的最新提交, 发布时 npm dist-tag 为 `dev`。

切换渠道 (git + npm): `openclaw update --channel stable|beta|dev`。
详情请参阅: [Development channels](https://docs.openclaw.ai/install/development-channels)。

## 从源码安装 (开发用)

从源码构建推荐使用 `pnpm`。Bun 是直接运行 TypeScript 的可选方案。

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw

pnpm install
pnpm ui:build # 首次运行时自动安装 UI 依赖
pnpm build

pnpm openclaw onboard --install-daemon

# 开发循环 (TS 更改时自动重新加载)
pnpm gateway:watch
```

注意: `pnpm openclaw ...` 会直接运行 TypeScript (通过 `tsx`)。`pnpm build` 会生成 `dist/` 目录，以便通过 Node 或打包后的 `openclaw` 二进制文件运行。

## 安全默认设置 (私聊访问)

OpenClaw 会连接到真实的即时通讯服务。请将收到的私聊消息视为 **不可信输入**。

完整安全指南: [Security](https://docs.openclaw.ai/gateway/security)

Telegram/WhatsApp/Signal/iMessage/Microsoft Teams/Discord/Google Chat/Slack 的默认行为:

- **私聊配对** (`dmPolicy="pairing"` / `channels.discord.dm.policy="pairing"` / `channels.slack.dm.policy="pairing"`): 未知发送者会收到一个简短的配对码，机器人不会处理他们的消息。
- 使用此命令批准: `openclaw pairing approve <channel> <code>` (随后发送者将被添加到本地允许列表存储中)。
- 公开接收私聊需要明确启用: 设置 `dmPolicy="open"` 并在渠道允许列表中包含 `"*"` (`allowFrom` / `channels.discord.dm.allowFrom` / `channels.slack.dm.allowFrom`)。

运行 `openclaw doctor` 以发现存在风险或配置错误的私聊策略。

## 亮点

- **[本地优先的 Gateway](https://docs.openclaw.ai/gateway)** — 会话、渠道、工具和事件的单一控制平面。
- **[多渠道收件箱](https://docs.openclaw.ai/channels)** — WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, BlueBubbles, Microsoft Teams, Matrix, Zalo, Zalo Personal, WebChat, macOS, iOS/Android。
- **[多智能体路由](https://docs.openclaw.ai/gateway/configuration)** — 将入站渠道/账户/对等点路由到隔离的智能体 (工作区 + 每个智能体的会话)。
- **[语音唤醒](https://docs.openclaw.ai/nodes/voicewake) + [对话模式](https://docs.openclaw.ai/nodes/talk)** — 适用于 macOS/iOS/Android 的始终在线语音功能，支持 ElevenLabs。
- **[实时 Canvas](https://docs.openclaw.ai/platforms/mac/canvas)** — 智能体驱动的可视化工作区，支持 [A2UI](https://docs.openclaw.ai/platforms/mac/canvas#canvas-a2ui)。
- **[一流的工具](https://docs.openclaw.ai/tools)** — 浏览器、Canvas、节点、cron、会话以及 Discord/Slack 动作。
- **[配套应用](https://docs.openclaw.ai/platforms/macos)** — macOS 菜单栏应用 + iOS/Android [节点](https://docs.openclaw.ai/nodes)。
- **[入职向导](https://docs.openclaw.ai/start/wizard) + [技能](https://docs.openclaw.ai/tools/skills)** — 向导驱动的设置，包含捆绑、托管和工作区技能。

## Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=openclaw/openclaw&type=date&legend=top-left)](https://www.star-history.com/#openclaw/openclaw&type=date&legend=top-left)

## 至今已构建的所有内容

### 核心平台

- [Gateway WS 控制平面](https://docs.openclaw.ai/gateway)，包含会话、在线状态、配置、cron、webhooks、[Control UI](https://docs.openclaw.ai/web) 和 [Canvas 宿主](https://docs.openclaw.ai/platforms/mac/canvas#canvas-a2ui)。
- [CLI 界面](https://docs.openclaw.ai/tools/agent-send): gateway, agent, send, [wizard](https://docs.openclaw.ai/start/wizard) 和 [doctor](https://docs.openclaw.ai/gateway/doctor)。
- [Pi 智能体运行时](https://docs.openclaw.ai/concepts/agent)，支持 RPC 模式、工具流式传输和块流式传输。
- [会话模型](https://docs.openclaw.ai/concepts/session): `main` 用于直接聊天、群组隔离、激活模式、队列模式、回复。群组规则请参阅: [Groups](https://docs.openclaw.ai/concepts/groups)。
- [媒体管道](https://docs.openclaw.ai/nodes/images): 图像/音频/视频、转录钩子、大小限制、临时文件生命周期。音频详情请参阅: [Audio](https://docs.openclaw.ai/nodes/audio)。

### 渠道

- [渠道](https://docs.openclaw.ai/channels): [WhatsApp](https://docs.openclaw.ai/channels/whatsapp) (Baileys), [Telegram](https://docs.openclaw.ai/channels/telegram) (grammY), [Slack](https://docs.openclaw.ai/channels/slack) (Bolt), [Discord](https://docs.openclaw.ai/channels/discord) (discord.js), [Google Chat](https://docs.openclaw.ai/channels/googlechat) (Chat API), [Signal](https://docs.openclaw.ai/channels/signal) (signal-cli), [iMessage](https://docs.openclaw.ai/channels/imessage) (imsg), [BlueBubbles](https://docs.openclaw.ai/channels/bluebubbles) (扩展), [Microsoft Teams](https://docs.openclaw.ai/channels/msteams) (扩展), [Matrix](https://docs.openclaw.ai/channels/matrix) (扩展), [Zalo](https://docs.openclaw.ai/channels/zalo) (扩展), [Zalo Personal](https://docs.openclaw.ai/channels/zalouser) (扩展), [WebChat](https://docs.openclaw.ai/web/webchat)。
- [群组路由](https://docs.openclaw.ai/concepts/group-messages): 提及门控、回复标签、每个渠道的分块和路由。渠道规则请参阅: [Channels](https://docs.openclaw.ai/channels)。

### 应用 + 节点

- [macOS 应用](https://docs.openclaw.ai/platforms/macos): 菜单栏控制平面, [语音唤醒](https://docs.openclaw.ai/nodes/voicewake)/一键通话 (PTT), [对话模式](https://docs.openclaw.ai/nodes/talk) 悬浮窗, [WebChat](https://docs.openclaw.ai/web/webchat), 调试工具, [远程网关](https://docs.openclaw.ai/gateway/remote) 控制。
- [iOS 节点](https://docs.openclaw.ai/platforms/ios): [Canvas](https://docs.openclaw.ai/platforms/mac/canvas), [语音唤醒](https://docs.openclaw.ai/nodes/voicewake), [对话模式](https://docs.openclaw.ai/nodes/talk), 摄像头, 屏幕录制, Bonjour 配对。
- [Android 节点](https://docs.openclaw.ai/platforms/android): [Canvas](https://docs.openclaw.ai/platforms/mac/canvas), [对话模式](https://docs.openclaw.ai/nodes/talk), 摄像头, 屏幕录制, 可选短信。
- [macOS 节点模式](https://docs.openclaw.ai/nodes): system.run/notify + canvas/camera 暴露。

### 工具 + 自动化

- [浏览器控制](https://docs.openclaw.ai/tools/browser): 专用的 openclaw Chrome/Chromium, 快照, 动作, 上传, 配置文件。
- [Canvas](https://docs.openclaw.ai/platforms/mac/canvas): [A2UI](https://docs.openclaw.ai/platforms/mac/canvas#canvas-a2ui) 推送/重置, eval, 快照。
- [节点](https://docs.openclaw.ai/nodes): 摄像头抓拍/裁剪, 屏幕录制, [location.get](https://docs.openclaw.ai/nodes/location-command), 通知。
- [Cron + 唤醒](https://docs.openclaw.ai/automation/cron-jobs); [Webhooks](https://docs.openclaw.ai/automation/webhook); [Gmail Pub/Sub](https://docs.openclaw.ai/automation/gmail-pubsub)。
- [技能平台](https://docs.openclaw.ai/tools/skills): 包含捆绑、托管和工作区技能，具有安装门控 + UI。

### 运行时 + 安全

- [渠道路由](https://docs.openclaw.ai/concepts/channel-routing), [重试策略](https://docs.openclaw.ai/concepts/retry) 和 [流式传输/分块](https://docs.openclaw.ai/concepts/streaming)。
- [在线状态](https://docs.openclaw.ai/concepts/presence), [正在输入提示](https://docs.openclaw.ai/concepts/typing-indicators) 和 [使用情况跟踪](https://docs.openclaw.ai/concepts/usage-tracking)。
- [模型](https://docs.openclaw.ai/concepts/models), [模型故障转移](https://docs.openclaw.ai/concepts/model-failover) 和 [会话修剪](https://docs.openclaw.ai/concepts/session-pruning)。
- [安全性](https://docs.openclaw.ai/gateway/security) 和 [故障排除](https://docs.openclaw.ai/channels/troubleshooting)。

### 运维 + 打包

- [Control UI](https://docs.openclaw.ai/web) + [WebChat](https://docs.openclaw.ai/web/webchat) 直接由 Gateway 提供。
- [Tailscale Serve/Funnel](https://docs.openclaw.ai/gateway/tailscale) 或 [SSH 隧道](https://docs.openclaw.ai/gateway/remote)，支持令牌/密码认证。
- [Nix 模式](https://docs.openclaw.ai/install/nix) 用于声明式配置; 基于 [Docker](https://docs.openclaw.ai/install/docker) 的安装。
- [Doctor](https://docs.openclaw.ai/gateway/doctor) 迁移, [日志记录](https://docs.openclaw.ai/logging)。

## 工作原理 (简述)

```
WhatsApp / Telegram / Slack / Discord / Google Chat / Signal / iMessage / BlueBubbles / Microsoft Teams / Matrix / Zalo / Zalo Personal / WebChat
               │
               ▼
┌───────────────────────────────┐
│            Gateway            │
│          (控制平面)           │
│     ws://127.0.0.1:18789      │
└──────────────┬────────────────┘
               │
               ├─ Pi 智能体 (RPC)
               ├─ CLI (openclaw …)
               ├─ WebChat UI
               ├─ macOS 应用
               └─ iOS / Android 节点
```

## 关键子系统

- **[Gateway WebSocket 网络](https://docs.openclaw.ai/concepts/architecture)** — 用于客户端、工具和事件的单一 WS 控制平面 (以及运维: [Gateway runbook](https://docs.openclaw.ai/gateway))。
- **[Tailscale 暴露](https://docs.openclaw.ai/gateway/tailscale)** — 用于 Gateway 仪表板 + WS 的 Serve/Funnel (远程访问: [Remote](https://docs.openclaw.ai/gateway/remote))。
- **[浏览器控制](https://docs.openclaw.ai/tools/browser)** — openclaw 管理的 Chrome/Chromium，带有 CDP 控制。
- **[Canvas + A2UI](https://docs.openclaw.ai/platforms/mac/canvas)** — 智能体驱动的可视化工作区 (A2UI 宿主: [Canvas/A2UI](https://docs.openclaw.ai/platforms/mac/canvas#canvas-a2ui))。
- **[语音唤醒](https://docs.openclaw.ai/nodes/voicewake) + [对话模式](https://docs.openclaw.ai/nodes/talk)** — 始终在线的语音和持续对话功能。
- **[节点](https://docs.openclaw.ai/nodes)** — Canvas, 摄像头抓拍/裁剪, 屏幕录制, `location.get`, 通知, 以及仅限 macOS 的 `system.run`/`system.notify`。

## Tailscale 访问 (Gateway 仪表板)

OpenClaw 可以自动配置 Tailscale **Serve** (仅限 tailnet) 或 **Funnel** (公开)，同时 Gateway 保持绑定到环回地址。配置 `gateway.tailscale.mode`:

- `off`: 无 Tailscale 自动化 (默认)。
- `serve`: 通过 `tailscale serve` 仅限 tailnet 的 HTTPS (默认使用 Tailscale 身份头)。
- `funnel`: 通过 `tailscale funnel` 的公开 HTTPS (需要共享密码认证)。

说明:

- 当启用 Serve/Funnel 时，`gateway.bind` 必须保持为 `loopback` (OpenClaw 会强制执行此操作)。
- 可以通过设置 `gateway.auth.mode: "password"` 或 `gateway.auth.allowTailscale: false` 来强制要求 Serve 使用密码。
- 除非设置了 `gateway.auth.mode: "password"`，否则 Funnel 拒绝启动。
- 可选: `gateway.tailscale.resetOnExit` 在关闭时撤销 Serve/Funnel。

详情请参阅: [Tailscale guide](https://docs.openclaw.ai/gateway/tailscale) · [Web surfaces](https://docs.openclaw.ai/web)

## 远程网关 (Linux 表现出色)

在小型 Linux 实例上运行 Gateway 是完全没问题的。客户端 (macOS 应用, CLI, WebChat) 可以通过 **Tailscale Serve/Funnel** 或 **SSH 隧道** 进行连接，并且在需要执行设备本地操作时，您仍然可以配对设备节点 (macOS/iOS/Android)。

- **网关宿主** 默认运行 exec 工具和渠道连接。
- **设备节点** 通过 `node.invoke` 运行设备本地动作 (`system.run`, 摄像头, 屏幕录制, 通知)。
  简而言之：exec 在 Gateway 所在地运行；设备动作在设备所在地运行。

详情请参阅: [Remote access](https://docs.openclaw.ai/gateway/remote) · [Nodes](https://docs.openclaw.ai/nodes) · [Security](https://docs.openclaw.ai/gateway/security)

## 通过 Gateway 协议的 macOS 权限

macOS 应用可以以 **节点模式** 运行，并通过 Gateway WebSocket 发布其功能 + 权限映射 (`node.list` / `node.describe`)。客户端随后可以通过 `node.invoke` 执行本地操作:

- `system.run` 运行本地命令并返回 stdout/stderr/退出代码; 设置 `needsScreenRecording: true` 以要求屏幕录制权限 (否则您将收到 `PERMISSION_MISSING`)。
- `system.notify` 发布用户通知，如果通知被拒绝则失败。
- `canvas.*`, `camera.*`, `screen.record` 和 `location.get` 同样通过 `node.invoke` 路由并遵循 TCC 权限状态。

提权的 bash (宿主权限) 与 macOS TCC 是分开的:

- 使用 `/elevated on|off` 来在启用并加入允许列表时切换每个会话的提权访问。
- Gateway 通过 `sessions.patch` (WS 方法) 将每个会话的开关与 `thinkingLevel`, `verboseLevel`, `model`, `sendPolicy` 和 `groupActivation` 一起持久化。

详情请参阅: [Nodes](https://docs.openclaw.ai/nodes) · [macOS app](https://docs.openclaw.ai/platforms/macos) · [Gateway protocol](https://docs.openclaw.ai/concepts/architecture)

## 智能体到智能体 (sessions\_\* 工具)

- 使用这些工具来协调跨会话的工作，而无需在聊天界面之间跳转。
- `sessions_list` — 发现活动的会话 (智能体) 及其元数据。
- `sessions_history` — 获取会话的转录日志。
- `sessions_send` — 向另一个会话发送消息; 可选的回复响应 + 宣告步骤 (`REPLY_SKIP`, `ANNOUNCE_SKIP`)。

详情请参阅: [Session tools](https://docs.openclaw.ai/concepts/session-tool)

## 技能注册表 (ClawHub)

ClawHub 是一个极简的技能注册表。启用 ClawHub 后，智能体可以自动搜索技能并在需要时引入新技能。

[ClawHub](https://clawhub.com)

## 聊天命令

在 WhatsApp/Telegram/Slack/Google Chat/Microsoft Teams/WebChat 中发送这些命令 (群组命令仅限所有者):

- `/status` — 紧凑的会话状态 (模型 + 令牌, 可用时显示成本)
- `/new` 或 `/reset` — 重置会话
- `/compact` — 压缩会话上下文 (总结)
- `/think <level>` — off|minimal|low|medium|high|xhigh (仅限 GPT-5.2 + Codex 模型)
- `/verbose on|off`
- `/usage off|tokens|full` — 每条响应的使用情况页脚
- `/restart` — 重启网关 (群组中仅限所有者)
- `/activation mention|always` — 群组激活切换 (仅限群组)

## 应用 (可选)

仅靠 Gateway 就能提供极佳的体验。所有应用都是可选的，并增加了额外的功能。

如果您计划构建/运行配套应用，请遵循下面的平台操作手册。

### macOS (OpenClaw.app) (可选)

- 菜单栏控制 Gateway 和运行状态。
- 语音唤醒 + 一键通话 (PTT) 悬浮窗。
- WebChat + 调试工具。
- 通过 SSH 远程控制网关。

注意: 需要经过签名的构建版本，以便 macOS 权限在重新构建后依然有效 (请参阅 `docs/mac/permissions.md`)。

### iOS 节点 (可选)

- 通过 Bridge 配对为节点。
- 语音触发转发 + Canvas 界面。
- 通过 `openclaw nodes …` 进行控制。

操作手册: [iOS connect](https://docs.openclaw.ai/platforms/ios)。

### Android 节点 (可选)

- 通过与 iOS 相同的 Bridge + 配对流程进行配对。
- 暴露 Canvas, 摄像头和屏幕截取命令。
- 操作手册: [Android connect](https://docs.openclaw.ai/platforms/android)。

## 智能体工作区 + 技能

- 工作区根目录: `~/.openclaw/workspace` (可通过 `agents.defaults.workspace` 配置)。
- 注入的提示词文件: `AGENTS.md`, `SOUL.md`, `TOOLS.md`。
- 技能: `~/.openclaw/workspace/skills/<skill>/SKILL.md`。

## 配置

最小化的 `~/.openclaw/openclaw.json` (模型 + 默认值):

```json5
{
  agent: {
    model: "anthropic/claude-opus-4-5",
  },
}
```

[完整配置参考 (所有键值 + 示例)。](https://docs.openclaw.ai/gateway/configuration)

## 安全模型 (重要)

- **默认情况:** 工具在 **main** 会话的宿主上运行，因此当只有您自己使用时，智能体拥有完整访问权限。
- **群组/渠道安全:** 设置 `agents.defaults.sandbox.mode: "non-main"` 以在每个会话的 Docker 沙箱中运行 **非主会话** (群组/渠道); 随后 bash 在这些会话的 Docker 中运行。
