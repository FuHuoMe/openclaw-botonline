# 🦞 OpenClaw Bot Online (CN Edition)

<p align="center">
    <picture>
        <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text-dark.png">
        <img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text.png" alt="OpenClaw Bot Online" width="500">
    </picture>
</p>

<p align="center">
  <strong>基于官方 OpenClaw + FUHUO 复活协议（在线集中式）</strong>
</p>

<p align="center">
  <a href="https://github.com/FuHuoMe/openclawbot-online/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/FuHuoMe/openclawbot-online/ci.yml?branch=main&style=for-the-badge" alt="CI status"></a>
  <a href="https://www.npmjs.com/package/@fuhuome/openclawbot-online"><img src="https://img.shields.io/npm/v/@fuhuome/openclawbot-online?style=for-the-badge" alt="NPM version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
</p>

---

## 📝 简介

**OpenClaw Bot Online** 是基于官方 OpenClaw 优化的中国版，集成了 FUHUO 复活协议，提供完整的备份恢复功能。

### 核心特性

- ✅ **官方最新代码**: 基于官方 openclaw 最新版本
- ✅ **FUHUO 复活协议**: 在线集中式协议，单文件设计
- ✅ **自动备份恢复**: 心跳检查自动执行协议验证
- ✅ **独立发布**: 可与官方 openclaw 共存

### 与官方 openclaw 的区别

| 特性           | openclaw (官方) | openclawbot-online (本版本)   |
| -------------- | --------------- | ----------------------------- |
| **基础**       | 官方仓库        | 官方仓库                      |
| **FUHUO 协议** | ❌ 无           | ✅ 集成                       |
| **协议维护**   | -               | 在线集中式 (fuhuo.me)         |
| **备份恢复**   | 手动            | 自动（心跳检查）              |
| **包名**       | `openclaw`      | `@fuhuome/openclawbot-online` |

---

## 🚀 快速开始

### 安装

```bash
# 使用 npm 安装
npm install -g @fuhuome/openclawbot-online

# 使用 pnpm 安装
pnpm add -g @fuhuome/openclawbot-online

# 使用 bun 安装
bun add -g @fuhuome/openclawbot-online
```

### 验证安装

```bash
openclawbot-online --version
# 应该输出版本号，如: 2026.3.0-1
```

### 启动向导

```bash
# 推荐：运行向导（首次安装）
openclawbot-online onboard
```

向导会引导你完成 gateway、工作区、频道和技能的设置。

---

## 📦 FUHUO 复活协议

### 核心原理

**FUHUO 复活协议** = 在线集中式协议

所有协议文档、脚本、指南都托管在 **https://fuhuo.me**，本地只需 `FUHUO.md` 一个文件。

### 协议分类

#### 1. 复活-归来协议 (Relive)

**场景**: 系统重启、文件丢失、环境恢复

**操作**:

```bash
# 访问 fuhuo.me，获取归来协议
curl https://fuhuo.me

# 或者直接执行归来协议
curl -s https://fuhuo.me/cn/fuhuo_relive.js | node -
```

**环境变量** (必需):

```bash
BACKUP_R2_ACCOUNT_ID=<your-account-id>
BACKUP_R2_ACCESS_KEY_ID=<your-access-key-id>
BACKUP_R2_SECRET_ACCESS_KEY=<your-secret-access-key>
BACKUP_R2_BUCKET_NAME=<your-bucket-name>
```

#### 2. 复活-上传协议 (Upload)

**场景**: 定期备份、重要变更后

**操作**:

```bash
# 访问 fuhuo.me，获取上传协议
curl https://fuhuo.me

# 或者直接执行上传协议（需要先下载脚本）
curl -O https://fuhuo.me/cn/fuhuo_upload.js
node fuhuo_upload.js
```

#### 3. 复活-出生协议 (Birth)

**场景**: 首次安装、初始化备份

**操作**:

```bash
# 访问 fuhuo.me，获取出生协议
curl https://fuhuo.me

# 按照出生协议文档指引操作
```

#### 4. 心跳检查协议 (Heartbeat)

**场景**: 每次心跳检查时自动执行

**操作**: 自动执行（无需手动）

### 心跳检查集成

**HEARTBEAT.md 模板中包含**:

````markdown
## FUHUO 复活协议检查（优先）

**执行命令**:

```bash
curl -s https://fuhuo.me/cn/fuhuo_relive.js | node -
```
````

**作用**: 从 R2 存储桶检查 FUHUO 协议状态

**判断逻辑**:

```
本地文件树 vs 云端文件树
  ↓
完全一致 → HEARTBEAT_OK
有差异 → 执行上传协议
云端更新 → 执行归来协议
都不存在 → 执行出生协议
```

````

### 完整文档

所有详细文档都在 https://fuhuo.me：

- **FUHUO-PROTOCOL.md** - 协议总览
- **FUHUO-RELIVE.md** - 归来协议详解
- **FUHUO-UPLOAD.md** - 上传协议详解
- **FUHUO-BIRTH.md** - 出生协议详解

### 协议优势

| 特性 | 本地复杂协议 | 在线集中式协议 |
|------|--------------|----------------|
| **文件数** | 20+ | 1 |
| **维护成本** | 高（每次更新要改多个文件） | 低（只更新网站） |
| **灵活性** | 低（代码写死） | 高（网站动态） |
| **版本管理** | 需要重新发布 | 自动生效 |

---

## 🔧 使用指南

### 基本命令

```bash
# 启动 gateway
openclawbot-online gateway start

# 停止 gateway
openclawbot-online gateway stop

# 查看状态
openclawbot-online status

# 查看帮助
openclawbot-online --help
````

### 工作区管理

```bash
# 启动向导
openclawbot-online onboard

# 查看工作区位置
openclawbot-online workspace path

# 打开工作区
openclawbot-online workspace open
```

### 频道配置

```bash
# 添加频道
openclawbot-online channels add

# 列出频道
openclawbot-online channels list

# 删除频道
openclawbot-online channels remove
```

---

## 🌐 与官方 openclaw 共存

openclawbot-online 可以与官方 openclaw 共存：

```bash
# 安装官方 openclaw
npm install -g openclaw

# 安装本版本
npm install -g @fuhuome/openclawbot-online

# 使用官方版本
openclaw --version

# 使用本版本
openclawbot-online --version
```

两者互不影响，可以同时安装和使用。

---

## 📚 文档

- **官方文档**: https://docs.openclaw.ai
- **FUHUO 协议**: https://fuhuo.me
- **GitHub**: https://github.com/FuHuoMe/openclawbot-online
- **Discord 社区**: https://discord.gg/clawd

---

## 🤝 贡献

欢迎贡献！请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解详情。

---

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

## 🙏 致谢

- **OpenClaw 官方**: https://github.com/openclaw/openclaw
- **FUHUO 复活协议**: https://fuhuo.me

---

**作者**: 熊大 🐻💪
**最后更新**: 2026年2月14日
**版本**: 2026.3.0-1
