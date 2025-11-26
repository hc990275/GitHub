<div align="center">

# 🐙 GitHub 管理器

### Cloudflare Worker 版

<br>

[![Cloudflare Workers](https://img.shields.io/badge/Cloudflare-Workers-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)](https://workers.cloudflare.com/)
[![GitHub API](https://img.shields.io/badge/GitHub-API-181717?style=for-the-badge&logo=github&logoColor=white)](https://docs.github.com/en/rest)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

<br>

**基于 Cloudflare Workers 的 GitHub 仓库在线管理工具**

🌍 **无需翻墙** 即可在国内管理你的 GitHub 仓库

<br>

[🚀 快速部署](#-快速部署) •
[✨ 功能特性](#-功能特性) •
[📱 使用说明](#-使用说明) •
[❓ 常见问题](#-常见问题)

<br>

---

**作者**：[hc990275](https://github.com/hc990275) • **项目地址**：[CF-Workers-GitHub-Manager](https://github.com/hc990275/CF-Workers-GitHub-Manager)

❤️ **分享是一种爱心，感谢你的支持与传播！**

---

</div>

<br>

## 🌟 为什么使用这个工具？

<table>
<tr>
<td width="50%">

### 🚫 痛点
- 国内访问 GitHub 慢或无法访问
- 手机/平板无法方便管理仓库
- 不想安装 Git 客户端
- 发布 Release 需要复杂操作

</td>
<td width="50%">

### ✅ 解决方案
- 通过 Cloudflare Workers 代理，**无需翻墙**
- 响应式网页，**任何设备**都能用
- 纯网页操作，**在线编辑保存**
- 支持**在线发布版本**并上传附件

</td>
</tr>
</table>

<br>

## ✨ 功能特性

<table>
<tr>
<td width="33%" valign="top">

### 📁 仓库管理

- 🌍 **无需翻墙** - 通过 CF Workers 代理
- 📁 **多仓库管理** - 自己的/Fork的/Star的
- 🌿 **分支切换** - 支持切换不同分支
- 🔍 **仓库搜索** - 搜索任意公开仓库
- ⭐ **Star/Fork** - 一键操作

</td>
<td width="33%" valign="top">

### ✏️ 文件编辑

- 📝 **在线编辑** - 支持任何文本文件
- 👁️ **Markdown 预览** - 实时渲染
- 💾 **快捷保存** - Ctrl+S 一键保存
- ➕ **新建文件/文件夹**
- ⬇️ **文件下载**

</td>
<td width="33%" valign="top">

### 📤 批量操作

- 📤 **批量上传** - 多文件同时上传
- 🗑️ **批量删除** - 文件/目录/仓库
- 📂 **目录折叠** - 抽屉式目录
- 🔍 **文件搜索** - 快速过滤

</td>
</tr>
<tr>
<td width="33%" valign="top">

### 🔗 文件分享

- 🔐 **签名保护** - 防止未授权访问
- ⚡ **实时更新** - 无延迟
- 🔄 **强制刷新** - 自动禁用缓存
- 📦 **Base64 编码** - 可选加密

</td>
<td width="33%" valign="top">

### 🚀 版本发布

- 🏷️ **创建 Release** - Tag/标题/说明
- 📎 **上传附件** - 支持多文件
- 📋 **草稿/预发布** - 灵活选项
- 📊 **版本管理** - 查看/删除

</td>
<td width="33%" valign="top">

### 🔐 权限管理

- 👑 **管理员** - 完全权限
- ✏️ **编辑者** - 读写权限
- 👁️ **只读** - 仅查看
- 🚶 **游客模式** - 无需登录浏览

</td>
</tr>
</table>

<br>

## 🔑 权限说明

| 权限等级 | 查看文件 | 编辑保存 | 新建删除 | 发布版本 | 删除仓库 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| 👑 **管理员** | ✅ | ✅ | ✅ | ✅ | ✅ |
| ✏️ **编辑者** | ✅ | ✅ | ✅ | ✅ | ❌ |
| 👁️ **只读** | ✅ | ❌ | ❌ | ❌ | ❌ |
| 🚶 **游客** | 仅列表 | ❌ | ❌ | ❌ | ❌ |

<br>

## 🚀 快速部署

### 步骤 1️⃣ 获取 GitHub Token

1. 打开 👉 https://github.com/settings/tokens
2. 点击 **Generate new token (classic)**
3. 配置权限：
   - **Note**: `Cloudflare GitHub Manager`
   - **Expiration**: 选择有效期
   - ✅ `repo` - 完整仓库访问（**必选**）
   - ✅ `delete_repo` - 删除仓库（可选）
   - ✅ `read:user` - 读取用户信息
4. 点击 **Generate token**
5. ⚠️ **立即复制 Token（只显示一次！）**

---

### 步骤 2️⃣ 部署到 Cloudflare

<details>
<summary><b>📌 方法一：控制台部署（推荐新手）</b></summary>

<br>

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 进入 **Workers & Pages** → **Create** → **Create Worker**
3. 给 Worker 起名，如 `github-manager`
4. 点击 **Edit code**
5. 删除默认代码，粘贴 `worker.js` 全部内容
6. 点击 **Deploy**

</details>

<details>
<summary><b>📌 方法二：Wrangler CLI 部署</b></summary>

<br>

```bash
# 安装 Wrangler
npm install -g wrangler

# 登录 Cloudflare
wrangler login

# 创建项目
mkdir github-manager && cd github-manager

# 复制 worker.js 到项目目录，然后部署
wrangler deploy
```

</details>

---

### 步骤 3️⃣ 配置环境变量

进入 Worker 的 **Settings** → **Variables and Secrets** → **Add**

#### 🔑 必需变量

| 变量名 | 说明 | 示例值 |
|--------|------|--------|
| `GITHUB_TOKEN` | GitHub Personal Access Token | `ghp_xxxxxxxxxxxx` |
| `TOKEN_ADMIN` | 管理员访问令牌（UUID） | `a1b2c3d4-e5f6-7890-abcd-ef1234567890` |
| `TOKEN_EDITOR` | 编辑者访问令牌（UUID） | `b2c3d4e5-f6g7-8901-bcde-f12345678901` |
| `TOKEN_READ` | 只读访问令牌（UUID） | `c3d4e5f6-g7h8-9012-cdef-123456789012` |

> 💡 **提示**：使用 [uuidgenerator.net](https://www.uuidgenerator.net/) 生成 UUID

#### 🎨 可选变量

| 变量名 | 说明 | 默认值 |
|--------|------|--------|
| `SHARE_SECRET` | 分享链接签名密钥 | `default-share-secret-change-me` |
| `FRIEND_LINKS` | 友情链接（JSON 数组） | `[]` |

<details>
<summary><b>📌 友情链接配置示例</b></summary>

```json
[
  {"name": "我的博客", "url": "https://blog.example.com"},
  {"name": "GitHub", "url": "https://github.com/hc990275"}
]
```

</details>

---

### 步骤 4️⃣ 访问使用

打开你的 Worker URL：

```
https://github-manager.你的账户.workers.dev
```

> 💡 **可选**：在 Worker 的 **触发器** → **自定义域** 中绑定你自己的域名

<br>

## 📱 使用说明

<details>
<summary><b>📁 仓库管理</b></summary>

<br>

- **切换仓库**：在左侧边栏顶部的下拉框中选择
- **复制仓库名**：点击下拉框旁边的 📋 按钮
- **搜索仓库**：点击 🔍 搜索仓库按钮，输入关键词
- **Star 仓库**：在仓库操作区点击 ⭐ Star
- **Fork 仓库**：在仓库操作区点击 🍴 Fork

</details>

<details>
<summary><b>🌿 分支操作</b></summary>

<br>

- **查看分支**：仓库选择下方有分支下拉框
- **切换分支**：选择不同分支，文件树自动刷新
- **注意**：所有操作（编辑、上传、删除）都基于当前选择的分支

</details>

<details>
<summary><b>✏️ 文件编辑</b></summary>

<br>

- **打开文件**：在文件树中点击文件名
- **编辑内容**：直接在右侧编辑器中修改
- **Markdown 预览**：`.md` 文件自动开启实时预览
- **保存文件**：点击 💾 保存按钮（或按 `Ctrl+S`）
- **下载文件**：点击 ⬇️ 下载按钮

</details>

<details>
<summary><b>📤 文件上传与新建</b></summary>

<br>

**上传文件：**
1. 点击左下角 📤 上传按钮
2. 选择目标目录
3. 选择一个或多个文件
4. 点击 📤 上传，等待进度条完成

**新建文件/文件夹：**
1. 点击左下角 ➕ 新建按钮
2. 选择类型（文件或文件夹）
3. 选择目标目录，输入名称
4. 点击 ✅ 创建

</details>

<details>
<summary><b>🗑️ 删除操作</b></summary>

<br>

1. 点击左下角 🗑️ 删除按钮
2. 选择删除类型：
   - **📄 文件** - 多选删除文件
   - **📁 目录** - 删除整个文件夹
   - **🗄️ 仓库** - 删除整个仓库（仅管理员）
3. 确认删除

> ⚠️ **删除操作不可恢复，请谨慎操作！**

</details>

<details>
<summary><b>🔗 文件分享</b></summary>

<br>

1. 点击左下角 📤 分享按钮
2. 选择要分享的文件
3. 可选择是否 Base64 编码
4. 点击 📋 复制链接

**链接格式：**
```
https://your-worker.dev/share/owner/repo/branch/path?sign=xxx
```

**特性：**
- ✅ 签名保护 - 防止未授权访问
- ✅ 实时更新 - 使用 GitHub API，无延迟
- ✅ 强制刷新 - 自动禁用缓存

</details>

<details>
<summary><b>🚀 版本发布（Releases）</b></summary>

<br>

1. 点击左下角 🚀 发布按钮
2. 切换到 ➕ 新建版本标签
3. 填写信息：
   - **Tag** - 版本标签（如 `v1.0.0`）
   - **标题** - 版本名称
   - **说明** - 更新日志（支持 Markdown）
   - **附件** - 可上传多个文件
   - **选项** - 草稿/预发布
4. 点击 🚀 发布

</details>

<br>

## 🌐 API 接口

| 接口 | 方法 | 说明 |
|------|------|------|
| `/api/repos` | GET | 获取所有仓库（分类） |
| `/api/search-repos` | GET | 搜索 GitHub 仓库 |
| `/api/star` | POST | 关注仓库 |
| `/api/unstar` | POST | 取消关注仓库 |
| `/api/fork` | POST | Fork 仓库 |
| `/api/tree` | GET | 获取仓库文件树 |
| `/api/file` | GET | 获取文件内容 |
| `/api/save` | POST | 保存文件 |
| `/api/delete-files` | DELETE | 删除多个文件 |
| `/api/delete-dir` | DELETE | 删除目录 |
| `/api/delete-repo` | DELETE | 删除仓库（需管理员） |
| `/api/releases` | GET/POST | 获取/创建 Release |
| `/api/upload-asset` | POST | 上传 Release 附件 |
| `/api/share-url` | GET | 生成分享链接 |
| `/api/verify` | GET | 验证 Token |
| `/api/friend-links` | GET | 获取友情链接 |

<br>

## ⚠️ 重要注意事项

<table>
<tr>
<td width="50%" valign="top">

### 🔐 安全相关

**GitHub Token 安全：**
- ❌ 不要泄露你的 GitHub Token
- ❌ 不要将 Token 提交到 Git 仓库
- ✅ 务必使用环境变量存储
- ✅ 定期更换 Token

**访问令牌安全：**
- ❌ 不要分享你的管理员 UUID
- ✅ 可以分享只读 UUID 给信任的人
- ✅ 使用强随机 UUID

</td>
<td width="50%" valign="top">

### 📊 配额限制

**GitHub API 限制：**
- 未认证：60 次/小时
- 认证：5000 次/小时

**Cloudflare Workers 限制：**
- 免费版：100,000 次请求/天
- 单次请求：10ms CPU 时间

**文件大小限制：**
- GitHub API：单文件最大 100MB
- 建议单文件不超过 10MB

</td>
</tr>
</table>

<br>

## ❓ 常见问题

<details>
<summary><b>Q: 提示 "GitHub Token 无效"？</b></summary>

**A:** 检查 `GITHUB_TOKEN` 环境变量是否正确配置，Token 是否过期。

</details>

<details>
<summary><b>Q: 仓库列表为空？</b></summary>

**A:** 检查 `GITHUB_TOKEN` 是否正确配置，Token 是否有 `repo` 权限。

</details>

<details>
<summary><b>Q: 保存失败提示无权限？</b></summary>

**A:** 确认使用 `TOKEN_ADMIN` 或 `TOKEN_EDITOR` 的值登录。

</details>

<details>
<summary><b>Q: 分享链接打开是 "无效的分享链接"？</b></summary>

**A:** 检查 `SHARE_SECRET` 是否被修改，修改后旧链接会失效。链接中的 `sign` 参数不能缺失或修改。

</details>

<details>
<summary><b>Q: 无法删除仓库？</b></summary>

**A:** 确保：
- 你是管理员角色
- GitHub Token 有 `delete_repo` 权限
- 正确输入了仓库名进行二次确认

</details>

<details>
<summary><b>Q: 上传文件失败？</b></summary>

**A:** 检查文件大小是否超过限制（建议不超过 10MB），Token 是否有 `repo` 权限。

</details>

<details>
<summary><b>Q: 友情链接不显示？</b></summary>

**A:** 检查 `FRIEND_LINKS` 环境变量是否为有效的 JSON 格式。

</details>

<br>

## 🛠 技术栈

<p align="center">
  <a href="https://workers.cloudflare.com/"><img src="https://img.shields.io/badge/Cloudflare-Workers-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Cloudflare Workers"></a>
  <a href="https://docs.github.com/en/rest"><img src="https://img.shields.io/badge/GitHub-API-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub API"></a>
  <a href="https://tailwindcss.com/"><img src="https://img.shields.io/badge/Tailwind-CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" alt="Tailwind CSS"></a>
  <a href="https://marked.js.org/"><img src="https://img.shields.io/badge/marked.js-Markdown-000000?style=for-the-badge" alt="marked.js"></a>
  <a href="https://highlightjs.org/"><img src="https://img.shields.io/badge/highlight.js-Code-3C4B64?style=for-the-badge" alt="highlight.js"></a>
</p>

<br>

## 🤝 贡献与反馈

欢迎提交 Issue 和 Pull Request！

<p align="center">
  <a href="https://github.com/hc990275/CF-Workers-GitHub-Manager/issues"><img src="https://img.shields.io/badge/📮_提交_Issue-blue?style=for-the-badge" alt="提交 Issue"></a>
  <a href="https://github.com/hc990275/CF-Workers-GitHub-Manager"><img src="https://img.shields.io/badge/⭐_Star_项目-yellow?style=for-the-badge" alt="Star 项目"></a>
</p>

<br>

## 📄 开源协议

本项目采用 **MIT License** 开源协议 - 自由使用、修改和分发。

<br>

---

<div align="center">

## 📞 联系方式

**作者**：[@hc990275](https://github.com/hc990275)

**项目主页**：[CF-Workers-GitHub-Manager](https://github.com/hc990275/CF-Workers-GitHub-Manager)

<br>

❤️ **分享是一种爱心，你的支持是我最大的动力！**

<br>

**感谢使用 GitHub 管理器！如有问题，欢迎随时联系！** 🎉

</div>