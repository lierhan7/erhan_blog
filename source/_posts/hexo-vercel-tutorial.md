---
title: Hexo + Vercel 个人技术博客搭建完整教程（2026 最新版）
date: 2026-02-01 12:24:16
tags:
  - Hexo
  - Vercel
categories: 
  - 教程
---

## 前期准备

### 1. 安装 Node.js

访问 [Node.js 官网](https://nodejs.org/)，下载并安装 **LTS 版本**（长期支持版）。

**验证安装：**
```bash
node -v
npm -v
```

看到版本号就说明安装成功。

### 2. 安装 pnpm（推荐）

pnpm 比 npm 更快、更省空间，强烈推荐使用。

```bash
npm install -g pnpm
```

**验证安装：**
```bash
pnpm -v
```

### 3. 安装 Git

访问 [Git 官网](https://git-scm.com/)，下载并安装。

**验证安装：**
```bash
git --version
```

### 4. 注册账号

- **GitHub 账号**：访问 [github.com](https://github.com) 注册
- **Vercel 账号**：访问 [vercel.com](https://vercel.com)，使用 GitHub 账号登录即可

---

## 安装 Hexo

### 1. 全局安装 Hexo CLI

```bash
npm install -g hexo-cli
```

### 2. 创建博客项目

```bash
# 创建名为 my-blog 的文件夹（可以改成你想要的名字）
hexo init my-blog

# 进入项目目录
cd my-blog

# ⚠️ 关键步骤：使用 pnpm 安装依赖
pnpm install
```

> **重要提示**：如果使用 `npm install` 可能会遇到依赖冲突错误，建议使用 `pnpm install` 或 `npm install --legacy-peer-deps`

### 3. 启动本地预览

```bash
pnpm exec hexo server
# 或简写
pnpm exec hexo s
```

在浏览器打开 `http://localhost:4000`，就能看到你的博客了！

按 `Ctrl+C` 停止服务。

---

## 本地配置博客

### 1. 修改基本配置

打开项目根目录的 `_config.yml` 文件，修改以下内容：

```yaml
# 网站信息
title: 我的技术博客          # 博客标题
subtitle: 记录学习与成长      # 副标题
description: 技术分享与总结   # 描述（用于 SEO）
keywords: 技术, 编程, 学习    # 关键词
author: 你的名字             # 作者
language: zh-CN              # 语言
timezone: Asia/Shanghai      # 时区

# URL 配置（先不填，部署后再改）
url: https://yourblog.vercel.app
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
pretty_urls:
  trailing_index: true
  trailing_html: true
```

### 2. 写第一篇文章

```bash
# 创建新文章
pnpm exec hexo new "我的第一篇博客"
```

这会在 `source/_posts/` 目录下创建一个 Markdown 文件，用任意文本编辑器打开：

```markdown
---
title: 我的第一篇博客
date: 2026-02-01 10:00:00
tags: 
  - 随笔
  - 开始
categories: 
  - 生活
comments: true
---

这是我的第一篇博客文章！

<!-- more -->

## 标题一

这里是正文内容...

### 标题二

可以插入代码：

​```python
def hello():
    print("Hello, World!")
​```

还可以插入图片、链接等。
```

### 3. 本地预览

```bash
# 清除缓存
pnpm exec hexo clean

# 生成静态文件
pnpm exec hexo generate
# 或简写
pnpm exec hexo g

# 启动本地服务器
pnpm exec hexo s
```

访问 `http://localhost:4000` 查看效果。

---

## 安装和配置主题

### 1. 安装 NexT 主题（推荐）

NexT 是最流行的 Hexo 主题之一。

```bash
# 安装 NexT 主题
pnpm add hexo-theme-next
```

### 2. 启用主题

编辑根目录的 `_config.yml`：

```yaml
# 找到 theme 配置项，修改为：
theme: next
```

### 3. 创建主题配置文件

在项目根目录创建 `_config.next.yml` 文件（与 `_config.yml` 同级）：

```yaml
# 主题方案
scheme: Muse  # 可选：Muse / Mist / Pisces / Gemini

# 菜单配置
menu:
  home: / || fa fa-home
  archives: /archives/ || fa fa-archive
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  about: /about/ || fa fa-user

# 侧边栏配置
sidebar:
  position: left
  display: post
  padding: 18
  offset: 12

# 头像
avatar:
  url: /images/avatar.jpg  # 替换成你的头像路径
  rounded: true
  rotated: false

# 社交链接
social:
  GitHub: https://github.com/你的用户名 || fab fa-github
  # E-Mail: mailto:你的邮箱 || fa fa-envelope
  # 其他社交链接...

# 文章底部标签图标
tag_icon: true

# 代码高亮主题
codeblock:
  theme:
    light: default
    dark: stackoverflow-dark
  copy_button:
    enable: true
```

### 4. 创建页面

```bash
# 创建标签页
pnpm exec hexo new page tags

# 创建分类页
pnpm exec hexo new page categories

# 创建关于页
pnpm exec hexo new page about
```

编辑生成的页面文件，设置页面类型：

**source/tags/index.md:**
```markdown
---
title: 标签
date: 2026-02-01
type: tags
comments: false
---
```

**source/categories/index.md:**
```markdown
---
title: 分类
date: 2026-02-01
type: categories
comments: false
---
```

**source/about/index.md:**
```markdown
---
title: 关于我
date: 2026-02-01
type: about
comments: false
---

这里写关于你的介绍...
```

---

## 集成 Waline 评论系统

### 1. 部署 Waline 服务端

1. 访问 [Vercel Waline 一键部署](https://vercel.com/new/clone?repository-url=https://github.com/walinejs/waline/tree/main/example)
2. 使用 GitHub 账号登录 Vercel
3. 点击 **Deploy**（部署）
4. 等待部署完成，会得到一个地址，例如：`https://your-waline.vercel.app`

### 2. 配置 LeanCloud 数据库（可选但推荐）

如果不配置数据库，评论数据会丢失。使用 LeanCloud 免费版即可。

1. 注册 [LeanCloud 国际版](https://console.leancloud.app)
2. 创建应用（开发版，免费）
3. 进入应用 → 设置 → 应用凭证，获取：
   - `App ID`
   - `App Key`
   - `Master Key`
4. 回到 Vercel，进入你的 Waline 项目
5. Settings → Environment Variables，添加：
   - `LEAN_ID`: 你的 App ID
   - `LEAN_KEY`: 你的 App Key
   - `LEAN_MASTER_KEY`: 你的 Master Key
6. 点击 **Redeploy** 重新部署

### 3. 安装 Waline 插件

⚠️ **这是关键步骤，很容易被忽略！**

```bash
# 安装 Hexo NexT Waline 插件
pnpm add @waline/hexo-next
```

### 4. 配置 Waline

编辑 `_config.next.yml`，添加或修改以下配置：

```yaml
# 评论系统配置
comments:
  style: tabs
  active: waline  # ← 这里必须设置为 waline
  storage: true
  lazyload: false

# Waline 配置
waline:
  enable: true
  serverURL: https://your-waline.vercel.app  # ← 替换成你的 Waline 地址
  pageview: true   # 文章阅读量统计
  comment: true    # 评论功能
  locale:
    placeholder: 欢迎评论，说说你的看法~
  emoji:
    - https://unpkg.com/@waline/emojis@1.2.0/weibo
    - https://unpkg.com/@waline/emojis@1.2.0/bilibili
  meta:
    - nick
    - mail
    - link
  requiredMeta:
    - nick
  wordLimit: 0
  pageSize: 10
```

### 5. 测试评论功能

```bash
pnpm exec hexo clean
pnpm exec hexo g
pnpm exec hexo s
```

访问任意文章页面（不是首页），应该能在底部看到 Waline 评论框了！

---

## 发布到 GitHub

### 1. 在 GitHub 创建仓库

1. 登录 GitHub
2. 点击右上角 `+` → `New repository`
3. 仓库名随意，比如 `my-blog`
4. 选择 **Public**（公开）
5. **不要**勾选 `Initialize this repository with a README`
6. 点击 `Create repository`

### 2. 初始化本地 Git 仓库

在博客项目目录执行：

```bash
# 初始化 Git
git init

# 添加所有文件
git add .

# 提交
git commit -m "Initial commit"

# 关联远程仓库（替换成你的 GitHub 用户名和仓库名）
git remote add origin https://github.com/你的用户名/my-blog.git

# 推送到 GitHub
git branch -M main
git push -u origin main
```

### 3. 配置 SSH（可选，避免每次输入密码）

```bash
# 生成 SSH 密钥
ssh-keygen -t ed25519 -C "your_email@example.com"

# 复制公钥
cat ~/.ssh/id_ed25519.pub
```

然后：
1. 访问 GitHub → Settings → SSH and GPG keys
2. 点击 **New SSH key**
3. 粘贴公钥，保存

修改远程仓库地址：
```bash
git remote set-url origin git@github.com:你的用户名/my-blog.git
```

---

## 部署到 Vercel

### 1. 导入项目

1. 登录 [Vercel](https://vercel.com)
2. 点击 `Add New...` → `Project`
3. 找到你的 `my-blog` 仓库，点击 `Import`

### 2. 配置构建设置

Vercel 通常会自动检测 Hexo 项目，但为了保险起见，确认以下配置：

- **Framework Preset**: Other
- **Build Command**: `pnpm exec hexo generate` 或 `hexo generate`
- **Output Directory**: `public`
- **Install Command**: `pnpm install`

> ⚠️ **重要提示**：如果你的项目中安装了 `hexo-renderer-pandoc`，必须先卸载，否则部署会失败！

```bash
# 检查是否安装了 pandoc 渲染器
pnpm list | grep pandoc

# 如果有，卸载它
pnpm remove hexo-renderer-pandoc

# 安装默认的 marked 渲染器
pnpm add hexo-renderer-marked

# 提交更改
git add .
git commit -m "fix: use marked renderer"
git push
```

### 3. 部署

点击 `Deploy`，等待几分钟，部署完成！

Vercel 会给你一个域名，类似：`https://my-blog-xxx.vercel.app`

### 4. 更新博客 URL

回到本地项目，修改 `_config.yml`：

```yaml
url: https://my-blog-xxx.vercel.app  # 替换成你的 Vercel 地址
```

重新提交到 GitHub：

```bash
git add .
git commit -m "update url"
git push
```

Vercel 会自动检测到更新并重新部署。

---

## 自定义域名（可选）

### 1. 购买域名

在阿里云、腾讯云、Namecheap、Cloudflare 等平台购买域名。

### 2. 在 Vercel 添加域名

1. 进入 Vercel 项目 → `Settings` → `Domains`
2. 输入你的域名，点击 `Add`
3. Vercel 会显示需要配置的 DNS 记录

### 3. 配置 DNS

在域名注册商的控制台添加 DNS 记录：

**方式一：A 记录**
- 类型：`A`
- 名称：`@`
- 值：`76.76.21.21`

**方式二：CNAME 记录**
- 类型：`CNAME`
- 名称：`@` 或 `www`
- 值：`cname.vercel-dns.com`

等待 DNS 生效（几分钟到几小时），然后就可以用你的域名访问博客了！

记得再次更新 `_config.yml` 中的 `url`：

```yaml
url: https://你的域名.com
```

---

## 日常使用

### 写新文章

```bash
# 创建新文章
pnpm exec hexo new "文章标题"

# 编辑文章
# 使用你喜欢的编辑器打开 source/_posts/文章标题.md
```

### 本地预览

```bash
# 清理缓存
pnpm exec hexo clean

# 生成静态文件
pnpm exec hexo g

# 启动本地服务器
pnpm exec hexo s
```

访问 `http://localhost:4000` 预览效果。

### 发布文章

```bash
# 提交到 GitHub
git add .
git commit -m "add: 新文章标题"
git push
```

推送后，Vercel 会自动检测更新并重新部署，几分钟后你的文章就会发布到线上！

### 管理评论

访问 Waline 管理后台：
```
https://your-waline.vercel.app/ui
```

可以查看、回复、删除评论。

---

## 常见问题

### 1. npm install 报错 "Cannot read properties of null"

**解决方案**：使用 pnpm 或添加参数

```bash
# 方案一：使用 pnpm（推荐）
pnpm install

# 方案二：使用 npm 加参数
npm install --legacy-peer-deps
```

### 2. Vercel 部署失败：Error: spawnSync pandoc ENOENT

**原因**：安装了 `hexo-renderer-pandoc`，但 Vercel 环境中没有 pandoc。

**解决方案**：卸载 pandoc 渲染器

```bash
pnpm remove hexo-renderer-pandoc
pnpm add hexo-renderer-marked
git add .
git commit -m "fix: use marked renderer"
git push
```

### 3. 评论不显示

**排查步骤**：

1. **确认安装了 Waline 插件**：
```bash
pnpm add @waline/hexo-next
```

2. **确认配置正确**：
   - `_config.next.yml` 中 `comments.active: waline`
   - `waline.enable: true`
   - `waline.serverURL` 填写正确

3. **清理缓存重新生成**：
```bash
pnpm exec hexo clean
pnpm exec hexo g
pnpm exec hexo s
```

4. **检查浏览器控制台**：
   - 按 F12 打开开发者工具
   - 切换到 Console 标签
   - 查看是否有错误信息

5. **确认访问的是文章页面**：
   - 评论只在文章页显示，不在首页显示

### 4. 推送到 GitHub 失败（权限问题）

**解决方案**：配置 SSH 密钥

```bash
# 生成 SSH 密钥
ssh-keygen -t ed25519 -C "your_email@example.com"

# 复制公钥
cat ~/.ssh/id_ed25519.pub

# 添加到 GitHub
# Settings → SSH and GPG keys → New SSH key

# 修改远程地址
git remote set-url origin git@github.com:你的用户名/my-blog.git
```

### 5. 如何插入图片？

**方式一：使用图床（推荐）**

上传图片到图床（如：SM.MS、ImgURL、七牛云），获取链接：

```markdown
![图片描述](https://example.com/image.jpg)
```

**方式二：本地图片**

1. 修改 `_config.yml`：
```yaml
post_asset_folder: true
```

2. 安装插件：
```bash
pnpm add hexo-asset-image
```

3. 创建文章时会生成同名文件夹，把图片放进去：
```
source/_posts/
  ├── my-post.md
  └── my-post/
      └── image.jpg
```

4. 在文章中引用：
```markdown
![图片描述](my-post/image.jpg)
```

### 6. 如何添加站点统计？

**Google Analytics：**

在 `_config.next.yml` 中配置：

```yaml
google_analytics:
  tracking_id: G-XXXXXXXXXX
  only_pageview: false
```

**百度统计：**

```yaml
baidu_analytics: xxxxxxxxxxxxxxxx
```

### 7. 如何优化 SEO？

1. **填写完整的站点信息**（`_config.yml`）：
```yaml
title: 你的博客名称
description: 详细的网站描述
keywords: 关键词1, 关键词2, 关键词3
```

2. **安装 SEO 插件**：
```bash
pnpm add hexo-generator-sitemap
pnpm add hexo-generator-feed
```

3. **配置 sitemap**（`_config.yml`）：
```yaml
sitemap:
  path: sitemap.xml

feed:
  type: atom
  path: atom.xml
  limit: 20
```

4. **提交到搜索引擎**：
   - Google Search Console: https://search.google.com/search-console
   - 百度站长平台: https://ziyuan.baidu.com

### 8. Vercel 自动部署不触发

**检查步骤**：

1. 确认 GitHub 仓库与 Vercel 项目已关联
2. 查看 Vercel 项目 → Settings → Git
3. 确认分支名称正确（通常是 `main` 或 `master`）
4. 手动触发部署：Deployments → Redeploy

---

## 进阶优化

### 1. 添加便捷脚本

编辑 `package.json`，在 `scripts` 部分添加：

```json
{
  "scripts": {
    "clean": "hexo clean",
    "build": "hexo generate",
    "dev": "hexo server",
    "deploy": "hexo deploy",
    "new": "hexo new"
  }
}
```

使用更简单的命令：

```bash
pnpm dev          # 启动本地服务器
pnpm build        # 生成静态文件
pnpm clean        # 清理缓存
```

### 2. 安装常用插件

```bash
# 文章字数统计
pnpm add hexo-word-counter

# 本地搜索
pnpm add hexo-generator-searchdb

# 图片懒加载
pnpm add hexo-lazyload-image

# 代码复制按钮（NexT 主题已内置）
# pnpm add hexo-prism-plugin
```

### 3. 配置本地搜索

在 `_config.next.yml` 中启用：

```yaml
local_search:
  enable: true
  trigger: auto
  top_n_per_article: 1
```

### 4. 添加阅读进度条

在 `_config.next.yml` 中配置：

```yaml
reading_progress:
  enable: true
  position: top
  color: "#37c6c0"
  height: 3px
```

### 5. 启用代码块复制按钮

在 `_config.next.yml` 中配置：

```yaml
codeblock:
  copy_button:
    enable: true
    show_result: true
    style: flat
```

---

## 快速命令参考

```bash
# Hexo 常用命令
pnpm exec hexo new "标题"       # 新建文章
pnpm exec hexo new page "页面"  # 新建页面
pnpm exec hexo clean            # 清理缓存
pnpm exec hexo generate         # 生成静态文件
pnpm exec hexo server           # 启动本地服务器
pnpm exec hexo g -d             # 生成并部署

# Git 常用命令
git add .                       # 添加所有更改
git commit -m "描述"            # 提交更改
git push                        # 推送到远程仓库
git pull                        # 拉取远程更新
git status                      # 查看状态

# pnpm 常用命令
pnpm install                    # 安装依赖
pnpm add 包名                   # 安装包
pnpm remove 包名                # 卸载包
pnpm update                     # 更新依赖
pnpm list                       # 查看已安装的包
```

---

## 🎉 总结

现在你已经拥有了一个：

✅ **完全免费**的个人技术博客  
✅ **自动化部署**（Git Push 即发布）  
✅ **HTTPS 支持**  
✅ **全球 CDN 加速**（Vercel）  
✅ **评论功能**（Waline）  
✅ **可自定义域名**  
✅ **SEO 优化**  

**下一步建议：**

1. 🎨 美化主题（探索 NexT 主题的各种配置）
2. 📊 配置网站统计（Google Analytics、百度统计）
3. 🔍 优化 SEO（提交到搜索引擎）
4. 📝 **开始认真写作！**（这是最重要的）

**写作建议：**

- 保持定期更新（每周 1-2 篇）
- 记录学习过程和技术心得
- 分享解决问题的经验
- 保持内容原创性
- 适当使用代码示例和图片

---

## 相关资源

- **Hexo 官方文档**：https://hexo.io/zh-cn/docs/
- **NexT 主题文档**：https://theme-next.js.org/docs/
- **Waline 官方文档**：https://waline.js.org/
- **Vercel 文档**：https://vercel.com/docs
- **Markdown 语法**：https://www.markdownguide.org/

---

有任何问题，欢迎：
- 查阅官方文档
- 在 GitHub 仓库提 Issue
- 在技术社区提问

祝你写作愉快！📝✨
