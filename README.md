# 🧞 OpenClaw Bot Online

**私有化部署的 AI 智能助手网关。**

> ⚠️ **声明：** 本项目基于 [jiulingyun/openclaw-cn](https://github.com/jiulingyun/openclaw-cn) 进行再开发，旨在提供更加灵活的在线服务部署方案。

<p align="center">
  <img src="docs/images/main-view.png" alt="OpenClaw Bot Online 控制界面" width="800">
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/openclaw-botonline"><img src="https://img.shields.io/npm/v/openclaw-botonline?style=for-the-badge&logo=npm&logoColor=white&label=npm" alt="npm 版本"></a>
  <a href="https://nodejs.org"><img src="https://img.shields.io/badge/Node.js-%E2%89%A5%2022-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node.js 版本"></a>
  <a href="https://github.com/FuHuoMe/openclaw-botonline"><img src="https://img.shields.io/github/stars/FuHuoMe/openclaw-botonline?style=for-the-badge&logo=github&label=Stars" alt="GitHub Stars"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/许可证-MIT-blue.svg?style=for-the-badge" alt="MIT 许可证"></a>
</p>

<p align="center">
  <a href="https://github.com/FuHuoMe/openclaw-botonline">📦 仓库</a> ·
  <a href="https://docs.openclaw.ai">📖 文档</a> ·
  <a href="https://github.com/FuHuoMe/openclaw-botonline/issues">💬 反馈</a>
</p>

---

## ✨ 特性

- **🚀 在线服务** — 支持云端部署和在线服务模式
- **🏠 本地优先** — 数据存储在你自己的设备上，隐私可控
- **📱 多渠道支持** — WhatsApp、Telegram、Slack、Discord、Signal、iMessage、飞书、微信（开发中）
- **🎙️ 语音交互** — macOS/iOS/Android 语音唤醒和对话
- **🖼️ Canvas 画布** — 智能体驱动的可视化工作区
- **🔧 技能扩展** — 内置技能 + 自定义工作区技能

## 🚀 快速开始

**环境要求：** Node.js ≥ 22

```bash
# 安装
npm install -g openclaw-botonline@latest

# 运行安装向导
openclaw-botonline onboard --install-daemon

# 启动网关
openclaw-botonline gateway --port 18789 --verbose
```

> 💡 **兼容性：** `clawdbot-online` 命令也可用，作为别名指向 `openclaw-botonline`。

## 📦 安装方式

### npm（推荐）

```bash
npm install -g openclaw-botonline@latest
# 或
pnpm add -g openclaw-botonline@latest
```

### 从源码构建

```bash
git clone https://github.com/FuHuoMe/openclaw-botonline.git
cd openclaw-botonline

pnpm install
pnpm ui:build
pnpm build

pnpm openclaw-botonline onboard --install-daemon
```

## 🔧 配置

最小配置 `~/.openclaw/openclaw.json`：

```json
{
  "agent": {
    "model": "anthropic/claude-opus-4-5"
  }
}
```

## 📚 文档

- [快速开始](https://clawd.org.cn/docs/start/getting-started)
- [Gateway 配置](https://clawd.org.cn/docs/gateway/configuration)
- [渠道接入](https://clawd.org.cn/docs/channels)
- [技能开发](https://clawd.org.cn/docs/tools/skills)

## 🔄 版本说明

本项目基于 [jiulingyun/openclaw-cn](https://github.com/jiulingyun/openclaw-cn) 进行再开发，适配在线服务部署场景。

版本格式：`v0.Y.Z`（如 `v0.1.4`）

## 🤝 参与贡献

欢迎提交 Issue 和 PR！

- Bug 修复和功能优化会考虑贡献回上游
- 翻译改进、文档完善、国内渠道适配都非常欢迎

## 📋 开发计划

- [x] CLI 界面汉化
- [x] Web 控制界面汉化
- [x] 配置向导汉化
- [x] 中文官网和文档
- [x] 飞书渠道适配
- [ ] 微信渠道适配
- [ ] QQ 渠道适配
- [ ] 钉钉/企业微信适配

## 📄 许可证

[MIT](LICENSE)

---

<p align="center">
  <strong>本项目基于 <a href="https://github.com/jiulingyun/openclaw-cn">jiulingyun/openclaw-cn</a> 进行再开发</a>
</p>

<p align="center">
  感谢原项目开发者 🧞
</p>
