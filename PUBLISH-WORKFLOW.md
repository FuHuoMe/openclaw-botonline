# OpenClaw Bot Online 发布流程文档

> 熊大的自动化发布指南 🐻💪

---

## 📋 前提条件

### 环境变量
```bash
# GitHub Token (用于创建仓库和推送)
export CODER_GITHUB_TOKEN="ghp_xxx..."

# npm Granular Access Token (必须启用 Bypass 2FA)
export CODER_NPM_TOKEN="npm_xxx..."
```

### npm Token 要求

**重要**: npm 在 2025-12-09 撤销了所有 Classic Tokens，现在必须使用 **Granular Access Token** 并启用 **Bypass 2FA**。

#### 创建 Granular Access Token

1. 访问: https://www.npmjs.com/settings/~/tokens
2. 点击 "Generate New Token" → "Granular Access Token"
3. 配置：
   - **Token name**: `openclaw-botonline-ci`
   - **Scope**: 选择 `openclaw-botonline` 包（或选择所有包）
   - **Permissions**: `Read & Write`
   - **Expiration**: `90 days`（最长）
   - **Bypass 2FA for CI/CD**: ✅ **必须勾选**
4. 点击 "Generate Token"
5. **立即复制** Token

---

## 🚀 完整发布流程

### 步骤 1: Fork 源仓库

```bash
# 设置源仓库
SOURCE_REPO="jiulingyun/openclaw-cn"
TARGET_REPO="FuHuoMe/openclaw-botonline"

# Clone 源仓库
cd /root/projects
git clone https://github.com/${SOURCE_REPO}.git ${TARGET_REPO}
cd ${TARGET_REPO}
```

### 步骤 2: 修改项目配置

#### 2.1 修改 package.json

```bash
# 修改包名和仓库信息
cat package.json | jq '
  .name = "openclaw-botonline" |
  .description = "OpenClaw Bot Online - Your AI assistant gateway" |
  .repository.url = "https://github.com/FuHuoMe/openclaw-botonline" |
  .bin = {
    "openclaw-botonline": "dist/entry.js",
    "clawdbot-online": "dist/entry.js"
  } |
  .homepage = "https://github.com/FuHuoMe/openclaw-botonline#readme"
' > package.json.tmp && mv package.json.tmp package.json
```

#### 2.2 修复 Workspace 依赖

```bash
# 替换所有子包的依赖
find . -name "package.json" -type f ! -path "*/node_modules/*" -exec sed -i 's/"openclaw-cn"/"openclaw-botonline"/g' {} \;

# 替换 workspace 依赖
find . -name "package.json" -type f ! -path "*/node_modules/*" -exec sed -i 's/workspace:openclaw-cn/workspace:openclaw-botonline/g' {} \;
```

### 步骤 3: 创建 GitHub 仓库

```bash
# 使用 GitHub API 创建仓库
curl -s -X POST \
  -H "Authorization: token ${CODER_GITHUB_TOKEN}" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/user/repos \
  -d '{
    "name": "openclaw-botonline",
    "description": "OpenClaw Bot Online - Your AI assistant gateway",
    "private": false,
    "has_issues": true,
    "has_projects": true,
    "has_wiki": false
  }'
```

### 步骤 4: 配置 Git 并推送

```bash
# 配置 Git 用户信息
git config user.email "fuhuome@tiwenti.chat"
git config user.name "FuHuoMe"

# 更新 remote URL
git remote set-url origin https://github.com/FuHuoMe/openclaw-botonline.git

# 提交更改
git add -A
git commit -m "chore: rename project to openclaw-botonline

- Update package.json name and metadata
- Change repository URL to FuHuoMe/openclaw-botonline
- Update bin commands
- Fix workspace dependencies"

# 推送到 GitHub
git push -u origin main
```

### 步骤 5: 安装依赖并构建

```bash
# 安装依赖
npm install

# 构建项目
npm run build

# 验证构建产物
ls -la dist/index.js
du -sh dist/
```

### 步骤 6: 发布到 npm

```bash
# 设置 npm Token
echo "//registry.npmjs.org/:_authToken=${CODER_NPM_TOKEN}" > .npmrc

# 发布到 npm
npm publish --access public --ignore-scripts

# 清理 .npmrc
rm -f .npmrc
```

### 步骤 7: 验证发布

```bash
# 查看 npm 包信息
npm view openclaw-botonline

# 访问包页面
# https://www.npmjs.com/package/openclaw-botonline
```

---

## 🔄 后续版本更新

### 更新版本号

```bash
# 补丁版本 (0.1.4 → 0.1.5)
npm version patch

# 次要版本 (0.1.4 → 0.2.0)
npm version minor

# 主要版本 (0.1.4 → 1.0.0)
npm version major
```

### 发布新版本

```bash
# 1. 提交更改
git add -A
git commit -m "chore: bump version to x.x.x"
git push

# 2. 发布到 npm
echo "//registry.npmjs.org/:_authToken=${CODER_NPM_TOKEN}" > .npmrc
npm publish --access public --ignore-scripts
rm -f .npmrc
```

---

## 🔧 故障排查

### 问题 1: 403 Forbidden - Bypass 2FA required

**错误**:
```
403 Forbidden - Two-factor authentication or granular access token with bypass 2FA enabled is required to publish packages.
```

**原因**: npm Token 没有启用 Bypass 2FA

**解决方案**:
1. 访问 https://www.npmjs.com/settings/~/tokens
2. 创建新的 Granular Access Token
3. **必须勾选** "Bypass 2FA for CI/CD"
4. 使用新 Token 重新发布

### 问题 2: Workspace 依赖错误

**错误**:
```
ERR_PNPM_WORKSPACE_PKG_NOT_FOUND
```

**原因**: package.json 中的 workspace 依赖名称不匹配

**解决方案**:
```bash
# 检查 workspace 依赖
grep -r "workspace:" extensions/*/package.json

# 替换所有 workspace 依赖
find extensions -name "package.json" -type f -exec sed -i 's/workspace:old-name/workspace:openclaw-botonline/g' {} \;
```

### 问题 3: 构建失败

**错误**:
```
sh: 1: tsc: not found
```

**原因**: 依赖未安装或 pnpm 环境问题

**解决方案**:
```bash
# 使用 npm 重新安装
npm install

# 或使用 pnpm
pnpm install

# 然后构建
npm run build
```

---

## 📊 发布检查清单

### 发布前检查

- [ ] 环境变量已设置 (`CODER_GITHUB_TOKEN`, `CODER_NPM_TOKEN`)
- [ ] npm Token 已启用 Bypass 2FA
- [ ] package.json 中的包名已更新
- [ ] 所有 workspace 依赖已修复
- [ ] 构建产物存在 (`dist/index.js`)
- [ ] GitHub 仓库已创建

### 发布后验证

- [ ] npm 包页面可访问
- [ ] `npm view openclaw-botonline` 返回正确信息
- [ ] GitHub 仓库代码已推送
- [ ] 可以通过 `npm install` 安装

---

## 📚 相关资源

- **GitHub 仓库**: https://github.com/FuHuoMe/openclaw-botonline
- **npm 包**: https://www.npmjs.com/package/openclaw-botonline
- **npm Token 指南**: `/root/clawd/NPM-TOKEN-GUIDE.md`
- **GitHub 配置**: `/root/clawd/GITHUB_CONFIG.md`

---

## 🎯 快速参考

### 一次性发布脚本

```bash
#!/bin/bash
set -e

# 配置
SOURCE_REPO="jiulingyun/openclaw-cn"
TARGET_REPO="FuHuoMe/openclaw-botonline"
PACKAGE_NAME="openclaw-botonline"

# 步骤 1: Clone
cd /root/projects
git clone https://github.com/${SOURCE_REPO}.git ${TARGET_REPO}
cd ${TARGET_REPO}

# 步骤 2: 修改配置
# (参见上面的详细步骤)

# 步骤 3: 创建 GitHub 仓库
# (参见上面的详细步骤)

# 步骤 4: 推送代码
# (参见上面的详细步骤)

# 步骤 5: 构建并发布
npm install
npm run build
echo "//registry.npmjs.org/:_authToken=${CODER_NPM_TOKEN}" > .npmrc
npm publish --access public --ignore-scripts
rm -f .npmrc

echo "✅ 发布完成！"
```

---

**文档版本**: v1.0
**最后更新**: 2026-02-13
**作者**: 熊大 🐻💪
