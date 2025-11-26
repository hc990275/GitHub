# 🐙 GitHub 管理器

基于 **Cloudflare Workers** 的 GitHub 仓库在线管理工具，**无需翻墙**即可在国内管理你的 GitHub 仓库。

![Cloudflare Workers](https://img.shields.io/badge/Cloudflare-Workers-F38020?logo=cloudflare)
![GitHub](https://img.shields.io/badge/GitHub-API-181717?logo=github)
![License](https://img.shields.io/badge/License-MIT-green)

**作者**: [hc990275](https://github.com/hc990275)

---

## 🌟 为什么使用这个工具？

| 痛点 | 解决方案 |
|------|----------|
| 🚫 国内访问 GitHub 慢或无法访问 | ✅ 通过 Cloudflare Workers 代理，**无需翻墙** |
| 📱 手机/平板无法方便管理仓库 | ✅ 响应式网页，**任何设备**都能用 |
| 🔧 不想安装 Git 客户端 | ✅ 纯网页操作，**在线编辑保存** |
| 📦 发布 Release 需要网页操作 | ✅ 支持**在线发布版本**并上传附件 |

---

## ✨ 功能特性

### 📁 仓库管理
- **自动获取仓库列表** - 无需手动配置，自动读取你的所有仓库
- **区分仓库类型** - 分别显示：我的仓库 / Fork 的仓库 / 关注的仓库
- **搜索 GitHub 仓库** - 搜索任意公开仓库
- **Star / Unstar** - 一键关注或取消关注仓库
- **Fork 仓库** - 一键 Fork 任意仓库到你的账户

### ✏️ 文件编辑
- **强制文本模式** - 类似 Notepad++，任何文件都能以文本方式打开
- **Markdown 预览** - 实时渲染，代码高亮
- **快捷保存** - Ctrl+S 一键保存到 GitHub
- **新建文件/文件夹** - 选择目录，创建新文件或文件夹

### 📂 文件夹折叠
- **抽屉式目录** - 点击文件夹展开/收起
- **全局展开/折叠** - 一键展开或折叠所有目录
- **文件搜索** - 快速过滤查找文件

### 🗑️ 删除管理
- **删除文件** - 多选批量删除
- **删除目录** - 删除整个文件夹及其内容
- **删除仓库** - 管理员可删除整个仓库（需确认）

### 📤 分享功能
- **签名保护** - 分享链接带签名，删除签名无法访问
- **Base64 编码** - 可选加密显示内容
- **支持所有文件** - 包括图片、二进制文件等

### 🚀 发布版本 (Releases)
- **创建 Release** - 填写 Tag、标题、说明
- **上传附件** - 支持多文件上传
- **草稿/预发布** - 灵活的发布选项
- **版本管理** - 查看和删除历史版本

### 🔐 权限控制
- **管理员** - 完全控制，可删除仓库
- **编辑者** - 编辑、保存、发布
- **只读** - 仅查看内容
- **游客** - 仅查看文件列表

---

## 🚀 快速部署

### 第一步：获取 GitHub Token

1. 打开 👉 https://github.com/settings/tokens
2. 点击 **Generate new token (classic)**
3. 配置权限：
   - **Note**: `Cloudflare GitHub Manager`
   - **Expiration**: 选择有效期
   - **勾选权限**:
     - ✅ `repo` - 完整仓库访问
     - ✅ `delete_repo` - 删除仓库（可选）
4. 点击 **Generate token**
5. **立即复制** Token（只显示一次！）

### 第二步：部署到 Cloudflare

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com)
2. 进入 **Workers & Pages** → **Create** → **Create Worker**
3. 给 Worker 起名，如 `github-manager`
4. 点击 **Edit code**
5. 删除默认代码，粘贴 `worker.js` 全部内容
6. 点击 **Deploy**

### 第三步：配置环境变量

进入 Worker 的 **Settings** → **Variables and Secrets** → **Add**

#### 必需变量

| 变量名 | 类型 | 说明 | 示例 |
|--------|------|------|------|
| `GITHUB_TOKEN` | Secret | GitHub 个人访问令牌 | `ghp_aBcDeFgHiJk...` |
| `TOKEN_ADMIN` | Secret | 管理员登录密钥 | `admin-550e8400-e29b` |
| `TOKEN_EDITOR` | Secret | 编辑者登录密钥 | `editor-6ba7b810-9dad` |
| `TOKEN_READ` | Secret | 只读用户登录密钥 | `read-6ba7b814-9dad` |

#### 可选变量

| 变量名 | 类型 | 说明 | 示例 |
|--------|------|------|------|
| `SHARE_SECRET` | Secret | 分享链接签名密钥 | `my-secret-key-123` |
| `FRIEND_LINKS` | Text | 友情链接 JSON | 见下方 |

**友情链接格式：**
```json
[{"name":"我的博客","url":"https://blog.example.com"},{"name":"GitHub","url":"https://github.com"}]
```

### 第四步：访问使用

打开你的 Worker URL：
```
https://github-manager.你的账户.workers.dev
```

---

## 📋 环境变量详解

### GITHUB_TOKEN

GitHub 个人访问令牌，用于调用 GitHub API。

**获取方式：**
1. GitHub → Settings → Developer settings → Personal access tokens
2. Generate new token (classic)
3. 勾选 `repo` 权限
4. 如需删除仓库功能，额外勾选 `delete_repo`

### TOKEN_ADMIN / TOKEN_EDITOR / TOKEN_READ

用户登录密钥，可以是任意字符串，推荐使用 UUID。

**生成 UUID：** https://www.uuidgenerator.net/

**登录时：** 输入对应的完整密钥值即可获得相应权限。

### SHARE_SECRET

分享链接的签名密钥，用于防止链接被猜测。

如果不配置，会使用默认密钥（不安全），建议自定义。

### FRIEND_LINKS

友情链接配置，JSON 数组格式，显示在侧边栏底部。

---

## 🔑 权限说明

| 权限等级 | 查看文件 | 编辑保存 | 新建删除 | 发布版本 | 删除仓库 |
|----------|----------|----------|----------|----------|----------|
| 👑 管理员 | ✅ | ✅ | ✅ | ✅ | ✅ |
| ✏️ 编辑者 | ✅ | ✅ | ✅ | ✅ | ❌ |
| 👁️ 只读 | ✅ | ❌ | ❌ | ❌ | ❌ |
| 🚶 游客 | 仅列表 | ❌ | ❌ | ❌ | ❌ |

---

## 📂 仓库分类

仓库选择器中会自动分类显示：

| 分类 | 说明 |
|------|------|
| 📁 **我的仓库** | 你创建的仓库 |
| 🍴 **Fork 的仓库** | 你 Fork 过来的仓库 |
| ⭐ **关注的仓库** | 你 Star 过的仓库 |

---

## 🔒 分享链接说明

### 链接格式
```
https://你的域名/share/owner/repo/branch/path/to/file?sign=abc123
```

### 参数说明
- `sign` - 必需，签名验证
- `encode=base64` - 可选，返回 Base64 编码内容

### 安全机制
- 删除 `sign` 参数 → 返回 403 错误
- 修改文件路径 → 签名不匹配，返回 403

---

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

---

## 💡 使用技巧

### 快捷键
- `Ctrl + S` - 保存文件
- `Enter` - 登录时按回车确认

### 搜索仓库
1. 点击仓库选择器旁边的 🔍 搜索
2. 输入关键词搜索 GitHub 公开仓库
3. 可以直接 Star 或 Fork 搜索结果

### 文件夹管理
- 点击文件夹名称展开/折叠
- 使用 "📂 展开" / "📁 折叠" 全局控制

---

## ❓ 常见问题

### Q: 仓库列表为空？
**A**: 检查 `GITHUB_TOKEN` 是否正确配置，Token 是否有 `repo` 权限。

### Q: 保存失败提示无权限？
**A**: 确认使用 `TOKEN_ADMIN` 或 `TOKEN_EDITOR` 的值登录。

### Q: 如何删除仓库？
**A**: 需要使用管理员权限登录，且 `GITHUB_TOKEN` 需要 `delete_repo` 权限。

### Q: 分享链接无法访问？
**A**: 检查链接是否完整，`sign` 参数不能缺失或修改。

### Q: Fork 的仓库不显示？
**A**: Fork 的仓库会自动显示在 "🍴 Fork 的仓库" 分组中。

---

## 🛠 技术栈

| 技术 | 用途 |
|------|------|
| [Cloudflare Workers](https://workers.cloudflare.com/) | 无服务器后端 |
| [GitHub API](https://docs.github.com/en/rest) | 仓库管理 |
| [Tailwind CSS](https://tailwindcss.com/) | UI 样式 |
| [marked.js](https://marked.js.org/) | Markdown 解析 |
| [highlight.js](https://highlightjs.org/) | 代码高亮 |

---

## 📄 许可证

MIT License - 自由使用、修改和分发。

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

**GitHub**: https://github.com/hc990275

---

## 📮 联系

如有问题，请在 [GitHub Issues](../../issues) 中反馈。
