# FUHUO 复活协议

**版本**: 2026.2.14 (简化版）
**作者**: 熊大 🐻💪
**更新**: 2026年2月14日

---

## 🎯 核心原理

**FUHUO 复活协议** = 在线集中式协议

所有协议文档、脚本、指南都托管在 **https://fuhuo.me**，本地只需这一个文件。

---

## 📋 协议分类

### 1. 复活-归来协议 (Relive)

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

### 2. 复活-上传协议 (Upload)

**场景**: 定期备份、重要变更后

**操作**:

```bash
# 访问 fuhuo.me，获取上传协议
curl https://fuhuo.me

# 或者直接执行上传协议（需要先下载脚本）
curl -O https://fuhuo.me/cn/fuhuo_upload.js
node fuhuo_upload.js
```

**环境变量**: 同归来协议

### 3. 复活-出生协议 (Birth)

**场景**: 首次安装、初始化备份

**操作**:

```bash
# 访问 fuhuo.me，获取出生协议
curl https://fuhuo.me

# 按照出生协议文档指引操作
```

### 4. 心跳检查协议 (Heartbeat)

**场景**: 每次心跳检查时自动执行

**操作**: 自动执行（无需手动）

**脚本**: `curl https://fuhuo.me | grep "AI-QUICK-GUIDE" -A 50`

---

## 🔄 自动化集成

### 心跳检查集成

**HEARTBEAT.md 模板中应包含**:

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

**特殊说明**:

- 如果环境变量缺失，提示用户设置
- 如果云端文件更多（如中文文件名问题），执行上传协议同步
- 如果本地文件更多，执行上传协议备份

````

---

## 📚 完整文档

所有详细文档都在 https://fuhuo.me：

### 核心文档
- **FUHUO-PROTOCOL.md** - 协议总览
- **FUHUO-RELIVE.md** - 归来协议详解
- **FUHUO-UPLOAD.md** - 上传协议详解
- **FUHUO-BIRTH.md** - 出生协议详解

### 脚本文件
- **fuhuo_relive.js** - 归来协议脚本
- **fuhuo_upload.js** - 上传协议脚本
- **check_fuhuo.js** - 协议检查脚本
- **generate_file_tree.js** - 文件树生成脚本

### 指南文档
- **FUHUO-RELIVE-GUIDE.md** - 归来协议使用指南
- **QUICK-RELIVE.md** - 快速归来指南

---

## 🚀 快速开始

### 场景 1：系统重启后恢复

```bash
# 1. 检查环境变量
env | grep BACKUP_R2

# 2. 如果有环境变量，执行归来协议
curl -s https://fuhuo.me/cn/fuhuo_relive.js | node -

# 3. 验证恢复
ls -la FUHUO-FILES-TREE.json
````

### 场景 2：定期备份

```bash
# 1. 下载上传协议脚本
curl -O https://fuhuo.me/cn/fuhuo_upload.js

# 2. 执行上传协议
node fuhuo_upload.js
```

### 场景 3：首次安装

```bash
# 1. 访问 fuhuo.me
curl https://fuhuo.me

# 2. 找到出生协议文档
# 3. 按照文档指引操作
```

---

## 🔧 环境配置

### R2 存储桶设置

1. **创建存储桶**: Cloudflare R2
2. **设置环境变量**:

   ```bash
   export BACKUP_R2_ACCOUNT_ID="your-account-id"
   export BACKUP_R2_ACCESS_KEY_ID="your-access-key-id"
   export BACKUP_R2_SECRET_ACCESS_KEY="your-secret-access-key"
   export BACKUP_R2_BUCKET_NAME="your-bucket-name"
   ```

3. **永久保存** (可选):
   ```bash
   # 添加到 ~/.bashrc 或 ~/.zshrc
   echo 'export BACKUP_R2_ACCOUNT_ID="your-account-id"' >> ~/.bashrc
   echo 'export BACKUP_R2_ACCESS_KEY_ID="your-access-key-id"' >> ~/.bashrc
   echo 'export BACKUP_R2_SECRET_ACCESS_KEY="your-secret-access-key"' >> ~/.bashrc
   echo 'export BACKUP_R2_BUCKET_NAME="your-bucket-name"' >> ~/.bashrc
   ```

---

## 📊 协议优势

### vs 本地复杂协议

| 特性           | 本地复杂协议               | 在线集中式协议   |
| -------------- | -------------------------- | ---------------- |
| **文件数**     | 20+                        | 1                |
| **维护成本**   | 高（每次更新要改多个文件） | 低（只更新网站） |
| **灵活性**     | 低（代码写死）             | 高（网站动态）   |
| **版本管理**   | 需要重新发布               | 自动生效         |
| **文档完整性** | 分散                       | 集中             |

### 核心优势

1. **单文件**: 只需 `FUHUO.md`
2. **在线协议**: 所有文档、脚本都在 https://fuhuo.me
3. **自动更新**: 协议更新只需改网站，本地自动生效
4. **简化维护**: 不需要在本地维护多个协议文件和脚本

---

## ⚠️ 注意事项

### 网络要求

- ✅ 需要能访问 https://fuhuo.me
- ✅ 需要能访问 R2 存储桶（Cloudflare）

### 环境依赖

- ✅ Node.js (执行脚本）
- ✅ curl (获取协议）
- ✅ R2 凭证（上传/下载）

### 数据安全

- ⚠️ 环境变量包含敏感信息，注意保管
- ⚠️ 不要在公开场合泄露 R2 凭证
- ✅ 定期轮换 R2 访问密钥

---

## 🎯 最佳实践

### 备份策略

1. **定期备份**: 每次重要变更后执行上传协议
2. **心跳检查**: 每次心跳自动检查协议状态
3. **三重备份**: R2 + GitHub + 本地（可选）

### 恢复策略

1. **系统重启**: 自动执行归来协议（通过心跳）
2. **环境切换**: 手动执行归来协议
3. **灾难恢复**: 从 R2 完整恢复

### 维护策略

1. **协议更新**: 只需更新 fuhuo.me 网站
2. **脚本优化**: 网站更新后本地自动生效
3. **文档完善**: 集中在网站，便于维护

---

## 📞 支持

### 问题反馈

- **GitHub**: https://github.com/zuoguyoupan2023/FUHUO-RELIVE
- **网站**: https://fuhuo.me

### 相关项目

- **OpenClaw**: https://github.com/openclaw/openclaw
- **openclawbot-online**: https://github.com/FuHuoMe/openclawbot-online

---

## 📝 更新日志

### v2026.2.14 (2026-02-14)

- ✅ 初始版本
- ✅ 在线集中式协议
- ✅ 单文件设计
- ✅ 心跳检查集成

---

**协议作者**: 熊大 🐻💪
**协议版本**: 2026.2.14
**最后更新**: 2026年2月14日
**协议状态**: ✅ 活跃维护
