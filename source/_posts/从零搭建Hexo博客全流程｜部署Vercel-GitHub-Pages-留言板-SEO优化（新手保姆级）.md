---
title: 从零搭建Hexo博客全流程｜部署Vercel+GitHub Pages+留言板+SEO优化（新手保姆级）
date: 2026-05-10 21:06:11
tags:
  - Hexo
  - 博客搭建
  - Vercel
  - GitHub Pages
  - SEO优化
  - 教程
categories:
  - 技术教程
cover: /img/hexo-blog-cover.jpg
description: 从零开始搭建个人博客的完整教程,包含Hexo安装、主题配置、Vercel和GitHub Pages双平台部署、Giscus留言板集成、SEO优化等全流程指南
---

> **摘要**：本文详细记录从0到1搭建Hexo静态博客的完整流程，包含环境搭建、主题配置、文章创建、双平台部署（Vercel+GitHub Pages）、Giscus留言板集成、SEO优化（站点地图、搜索引擎提交），每步附具体命令和操作提示，新手可直接跟着复制操作，全程无坑，最终实现博客线上可访问、可留言、可被搜索引擎收录。
>
> **关键词**：Hexo | Vercel部署 | GitHub Pages | Giscus留言板 | Hexo SEO优化 | 新手博客搭建

## 前言

作为新手，想拥有一个属于自己的个人博客，无需复杂的后端开发，**Hexo + Vercel/GitHub Pages 是最优选择**——免费、高效、易维护。

本文整合了搭建过程中的所有关键步骤，解决了新手常见的部署报错、留言板不显示、SEO不生效等问题，**全程手把手教学**，跟着做就能成功搭建属于自己的个人博客。

---

## 一、前期准备（必做，5分钟搞定）

搭建 Hexo 博客前，需要先安装两个基础工具，全程下一步安装即可，无需复杂配置。

### 1.1 安装 Node.js（Hexo 运行依赖）

Hexo 基于 Node.js 运行，必须先安装 Node.js，版本建议选择 **16.x 及以上**（稳定不报错）。

📥 **下载地址**：<https://nodejs.org/zh-cn/>

💡 **操作提示**：
- 选择"长期支持版（LTS）"
- 下载后双击安装，全程默认下一步
- 安装完成后，打开终端验证是否成功

**验证命令：**
```bash
node -v
npm -v
```

若能正常显示版本号（如 `v18.16.0`、`9.8.1`），则安装成功。

### 1.2 安装 Git（版本控制+部署依赖）

Git 用于将本地博客代码推送到 GitHub，后续部署 GitHub Pages 和 Vercel 都需要用到。

📥 **下载地址**：<https://git-scm.com/downloads>

💡 **操作提示**：
- 下载对应系统版本（Windows/Mac）
- 安装时勾选 **"Add Git to PATH"**（方便终端直接使用 Git 命令）
- 其余默认下一步

**验证命令：**
```bash
git --version
```

能显示 Git 版本号（如 `git version 2.40.1`），即为安装成功。

### 1.3 注册必备账号（免费）

后续部署和留言板需要用到两个账号，提前注册好：

| 平台 | 用途 | 注册地址 |
|------|------|----------|
| **GitHub** | 托管博客代码、搭建 GitHub Pages、集成 Giscus 留言板 | <https://github.com/> |
| **Vercel** | 快速部署 Hexo 博客，支持自动更新 | <https://vercel.com/> |

 **建议**：Vercel 账号建议用 GitHub 账号直接登录，后续部署更便捷。

---

## 二、搭建 Hexo 本地博客（核心步骤）

这一步完成后，就能在本地预览自己的博客了，全程使用终端命令，复制即可执行。

### 2.1 安装 Hexo 脚手架（全局安装）

打开终端，输入以下命令，全局安装 Hexo

💡 **国内用户优化**：若安装缓慢，可先切换淘宝镜像：
```bash
npm config set registry https://registry.npmmirror.com
```

**安装命令：**
```bash
npm install -g hexo-cli
```

**验证命令：**
```bash
hexo -v
```

显示 Hexo 版本号及相关依赖信息，即为安装成功。

### 2.2 初始化 Hexo 博客（创建本地项目）

1️⃣ **新建文件夹**：在电脑上新建一个文件夹（如 `HexoBlog`），用于存放博客所有文件

2️ **切换到该文件夹**（以 `D:\HexoBlog` 为例）：
```bash
cd D:\HexoBlog
```

3️⃣ **初始化 Hexo 博客**：
```bash
hexo init
```

执行完成后，Hexo 会自动生成博客的基础目录结构，等待终端显示 `Start blogging with Hexo!`，即为初始化成功。

### 2.3 本地预览 Hexo 博客

初始化完成后，依次执行以下命令：

```bash
hexo clean   # 清理缓存（首次可省略，后续更新建议必执行）
hexo g       # 生成静态页面（简写，全称 hexo generate）
hexo s       # 启动本地服务（简写，全称 hexo server）
```

终端显示 `Hexo is running at http://localhost:4000`，说明服务启动成功

🌐 **访问地址**：<http://localhost:4000>

至此，本地博客搭建完成！

### 2.4 更换 Butterfly 主题（推荐，更美观）

Hexo 默认主题较简洁，新手推荐使用 Butterfly 主题（美观、易配置、支持多种功能）。

**安装命令：**
```bash
npm install hexo-theme-butterfly --save
```

**修改配置**：打开博客根目录下的 `_config.yml`（站点配置文件），找到 `theme` 字段：

```yaml
theme: butterfly  # 替换默认的 theme: landscape
```

**重新启动服务：**
```bash
hexo clean && hexo g && hexo s
```

刷新浏览器，就能看到 Butterfly 主题的博客页面，后续所有配置都基于该主题进行。

---

## 三、创建第一篇博客文章（新手必学）

Hexo 创建文章非常简单，使用命令自动生成文章模板，编辑后即可预览。

### 3.1 生成文章模板

```bash
hexo new "免费版Navicat｜Navicat Premium Lite 17 下载安装+使用教程"
```

执行完成后，文章会自动生成在 `source/_posts/` 目录下，文件格式为 Markdown（`.md`），文件名会自动处理特殊字符（如 `｜` 替换为 `-`）。

### 3.2 编辑文章内容

1️⃣ **打开文章文件**：进入 `source/_posts/` 目录，找到生成的 `.md` 文件

2️ **配置 Front-Matter**（文章顶部用 `---` 包裹的部分）：

```yaml
---
title: 免费版Navicat｜Navicat Premium Lite 17 下载安装+使用教程
date: 2026-05-10 15:30:00  # 文章发布日期，可自定义
tags:
  - 数据库工具
  - Navicat
categories:
  - 软件教程
cover:  # 可选，文章封面图，可填写图片URL
description: 分享免费版 Navicat Premium Lite 17 下载、详细安装步骤及基础使用入门教程，零基础也能快速上手。
---
```

3️⃣ **编辑文章内容**（在 `---` 下方，使用 Markdown 语法）：

```markdown
## 一、软件介绍
Navicat Premium Lite 17 是一款免费的数据库管理工具，支持MySQL、SQL Server等多种数据库，适合新手使用。

## 二、下载地址
官方下载地址：xxx

## 三、安装步骤
1. 双击安装包，选择安装路径
2. 点击"下一步"，完成安装
3. 启动软件，无需激活，直接使用

## 四、基础使用
### 4.1 连接MySQL数据库
1. 打开Navicat，点击"连接"→"MySQL"
2. 输入数据库地址、用户名、密码，点击"确定"
3. 连接成功后，即可管理数据库
```

### 3.3 本地预览文章

编辑完成后，重新生成并预览：

```bash
hexo clean && hexo g && hexo s
```

打开 <http://localhost:4000>，点击"归档"或直接访问文章链接，就能看到编辑好的文章。

---

## 四、部署 Hexo 博客到 Vercel（推荐，快速生效）

Vercel 是一款免费的静态网站托管平台，支持 Hexo 自动部署，无需复杂配置，部署后可获得一个免费域名。

### 4.1 准备博客代码（关联 GitHub）

1️⃣ **在 GitHub 上新建仓库**：
- 登录 GitHub，点击"New repository"
- 仓库名可自定义（如 `xuan-blog`）
- 选择 **Public**（公开）
- 点击"Create repository"

2️⃣ **初始化 Git 并推送**：

```bash
# 初始化 Git 仓库
git init

# 添加所有博客文件到暂存区
git add .

# 提交文件
git commit -m "init hexo blog"

# 关联 GitHub 仓库（替换为你的仓库地址）
git remote add origin git@github.com:xuanbin/xuan-blog.git

# 推送到 GitHub（首次推送，可能需要输入 GitHub 账号密码/验证）
git push -u origin main
```

💡 **提示**：首次推送若出现安全提示 `The authenticity of host 'github.com' can't be established.`，输入 `yes` 按回车即可，后续不会再出现。

### 4.2 部署到 Vercel

1️⃣ 登录 Vercel（用 GitHub 账号登录）

2️⃣ 点击右上角 **"New Project"**

3️⃣ 点击 **"Import from GitHub"**，选择你的博客仓库，点击"Import"

4️⃣ **配置部署参数**（默认即可，无需修改）：
- **Framework Preset**：选择"Hexo"（Vercel 会自动识别）
- **Build Command**：默认 `hexo generate`
- **Output Directory**：默认 `public`

5️⃣ 点击 **"Deploy"**，等待 1-2 分钟

部署完成后，Vercel 会生成一个免费域名（如 `xuan-blog.vercel.app`），点击即可访问线上博客！

### 4.3 后续更新文章（自动部署）

后续编辑文章或修改配置后，只需执行：

```bash
git add .
git commit -m "更新文章/修改配置"
git push
```

Vercel 会监听 GitHub 仓库变化，**自动重新部署**，无需手动操作！

---

## 五、部署到 GitHub Pages（备用，双平台保障）

为了保障博客稳定性，可同时部署到 GitHub Pages（免费托管），作为 Vercel 的备用地址。

### 5.1 新建 GitHub Pages 专用仓库

登录 GitHub，新建一个仓库，**仓库名必须为 `你的GitHub用户名.github.io`**（如 `xuanbin.github.io`），选择"Public"。

⚠️ **重要**：仓库名必须严格按照这个格式，否则 GitHub Pages 无法正常生效。

### 5.2 安装 Hexo 部署插件

```bash
npm install hexo-deployer-git --save
```

### 5.3 配置站点配置文件

打开博客根目录下的 `_config.yml`，拉到最底部，找到 `deploy` 字段：

```yaml
deploy:
  type: git
  repo: git@github.com:xuanbin/xuanbin.github.io.git  # 替换为你的仓库地址
  branch: main
```

### 5.4 一键部署到 GitHub Pages

```bash
hexo clean && hexo g && hexo d
```

部署完成后，等待 **1-5 分钟**（GitHub Pages 生效需要时间），访问地址：`https://你的GitHub用户名.github.io`

💡 **提示**：后续更新文章，执行同样的命令即可同步更新 GitHub Pages 上的内容。

---

## 六、集成 Giscus 留言板（实现博客留言功能）

推荐使用 **Giscus**（基于 GitHub Discussions，免费、稳定、无广告），替代传统评论系统。

### 6.1 启用 GitHub 仓库 Discussions 功能

1️⃣ 登录 GitHub，进入你的博客仓库

2️⃣ 点击 **"Settings"** → 找到 **"Features"** 板块

3️⃣ 勾选 **"Discussions"**，点击"Save"

### 6.2 安装 Giscus App

1️⃣ 打开 Giscus App 页面：<https://github.com/apps/giscus>

2️ 点击右上角 **"Install"**

3️ 选择"Only select repositories"，勾选你的博客仓库

4️⃣ 点击 **"Install"**，完成授权

### 6.3 获取 Giscus 配置参数

1️ 打开 Giscus 官网：<https://giscus.app/zh-CN>

2️⃣ **配置参数**：
- **Repository**：输入你的博客仓库（如 `xuanbin/xuan-blog`）
- **页面讨论**：选择"路径名称（pathname）"
- **分类**：选择"Announcements"

3️⃣ 配置完成后，提取 **4 个关键参数**：
- `repo`
- `repo_id`
- `category`
- `category_id`

### 6.4 配置 Butterfly 主题启用 Giscus

打开 `_config.butterfly.yml`，找到 `comments` 和 `giscus` 板块：

```yaml
# 评论配置
comments:
  use: giscus
  text: true
  lazyload: false
  count: true
  nav: false

# Giscus配置
giscus:
  repo: xuanbin/xuan-blog
  repo_id: R_kgDOSYzXJA
  category: Announcements
  category_id: DIC_kwDOSYzXJM4C8s2C
  mapping: pathname
  strict: 0
  reactions_enabled: 1
  emit_metadata: 0
  input_position: bottom
  theme: preferred_color_scheme
  lang: zh-CN
  crossorigin: anonymous
```

⚠️ **注意**：替换上述参数为你获取到的真实 Giscus 参数！

### 6.5 本地预览 + 部署上线

```bash
# 本地预览
hexo clean && hexo g && hexo s

# 部署上线
git add .
git commit -m "feat: 集成Giscus留言板"
git push
hexo clean && hexo g && hexo d
```

打开文章页面，拉到最底部，就能看到 Giscus 留言框，支持 GitHub 账号登录留言。

### 6.6 创建独立留言板页面（可选）

若想添加一个独立的留言板页面（导航栏显示）：

```bash
hexo new page "message"
```

打开 `source/message/index.md`，修改为：

```yaml
---
title: 留言板
date: 2026-05-10 15:00:00
comments: true  # 启用留言功能
---

在这里可以留言、交流、提建议～
```

在 `_config.butterfly.yml` 的 `menu` 板块添加导航：

```yaml
menu:
  首页: /
  归档: /archives/
  标签: /tags/
  分类: /categories/
  留言板: /message/
```

部署后，导航栏会显示"留言板"，点击即可进入独立留言页面。

---

## 七、SEO 优化（让搜索引擎收录你的博客）

搭建好博客后，需要进行 SEO 优化，让百度、谷歌等搜索引擎能找到你的博客，提升曝光率。

### 7.1 生成站点地图（sitemap）

站点地图用于告诉搜索引擎博客的页面结构，方便爬虫抓取。

**安装插件：**
```bash
npm install hexo-generator-sitemap --save          # 通用版（谷歌、必应）
npm install hexo-generator-baidu-sitemap --save    # 百度专用版
```

**修改 `_config.yml`，在末尾添加：**
```yaml
# 站点地图配置
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```

**生成站点地图：**
```bash
hexo clean && hexo g
```

生成后，在 `public/` 目录下会出现 `sitemap.xml` 和 `baidusitemap.xml` 两个文件。

**线上访问地址：**
- 通用版：`https://你的域名/sitemap.xml`
- 百度版：`https://你的域名/baidusitemap.xml`

### 7.2 提交站点地图到搜索引擎

#### 提交到百度（国内流量核心）

1️ 打开百度搜索资源平台：<https://ziyuan.baidu.com/>

2️ 点击"用户中心"→"站点管理"→"添加网站"

3️⃣ 完成站点验证（推荐 HTML 文件验证）

4️⃣ 进入站点后台，找到"站点地图"，提交：`https://你的域名/baidusitemap.xml`

#### 提交到谷歌（国际流量补充）

1️⃣ 打开谷歌搜索控制台：<https://search.google.com/search-console/>

2️ 选择"网址前缀"，输入你的博客域名

3️⃣ 完成验证后，左侧菜单找到"站点地图"

4️⃣ 输入 `sitemap.xml`，点击"提交"

### 7.3 其他 SEO 优化细节（提升收录率）

✅ **1. 配置 robots.txt 文件**

在 `source/` 目录新建 `robots.txt` 文件：

```txt
User-agent: *
Allow: /
Sitemap: https://xuan-blog.vercel.app/sitemap.xml
Sitemap: https://xuan-blog.vercel.app/baidusitemap.xml
```

✅ **2. 优化文章标题和描述**

- 每篇文章的 Front-Matter 中填写 `description` 字段
- 标题包含核心关键词（如"Navicat 安装教程"）
- 避免堆砌关键词

✅ **3. 持续更新内容**

定期发布新文章，Hexo 会自动更新站点地图，搜索引擎会更频繁地抓取你的博客。

✅ **4. 优化 URL 结构**

打开 `_config.yml`，修改 `permalink` 为简洁格式：

```yaml
permalink: :title.html  # 简化 URL，仅保留文章标题
```

---

## 八、常见问题排查（新手必看）

###  问题 1：本地预览看不到 Giscus 留言框？

**解决方法：**
1. 检查 `_config.butterfly.yml` 中 `comments.use` 是否为 `giscus`
2. 确保 Giscus 参数填写正确
3. 文章 Front-Matter 中没有 `comments: false`
4. 执行 `hexo clean` 清理缓存
5. ⚠️ 留言框只在文章页面和独立留言板显示，首页不显示

### ❓ 问题 2：部署到 Vercel/GitHub Pages 后，页面空白？

**解决方法：**
1. 检查 `_config.yml` 中 `url` 字段是否填写正确（如 `https://xuan-blog.vercel.app`）
2. 执行 `hexo clean && hexo g` 重新打包
3. 查看 Vercel 部署日志，检查主题是否安装成功

###  问题 3：提交站点地图后，搜索引擎不收录？

**解决方法：**
1. 收录需要时间（1-7 天），耐心等待
2. 在搜索引擎输入 `site:你的域名` 查看收录情况
3. 检查站点地图是否能正常访问
4. 百度可使用"主动推送"功能，加快收录

###  问题 4：推送 Git 时，提示"Permission denied"？

**解决方法：**
- 配置 GitHub SSH 密钥
- 参考 GitHub 官方文档配置完成后，即可正常推送

---

## 九、总结

本文从前期准备、本地搭建、文章创建，到双平台部署（Vercel+GitHub Pages）、Giscus 留言板集成、SEO 优化，**完整覆盖了 Hexo 博客搭建的全流程**。

每步都给出了具体命令和操作提示，新手可直接跟着复制操作。搭建完成后，你拥有的不仅是一个可线上访问的个人博客，还有稳定的留言功能和完善的 SEO 优化。

后续只需**持续更新文章**，就能让更多人看到你的内容！

---

##  核心命令汇总（方便快速复制）

```bash
# 1. 安装 Hexo 及相关插件
npm install -g hexo-cli
npm install hexo-theme-butterfly --save
npm install hexo-deployer-git --save
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save

# 2. 新建文章
hexo new "文章标题"

# 3. 本地预览
hexo clean && hexo g && hexo s

# 4. 部署到 GitHub Pages
hexo clean && hexo g && hexo d

# 5. Git 提交（同步到 Vercel）
git add .
git commit -m "备注信息"
git push
```

 **点赞+收藏**，后续搭建博客更方便！

如果搭建过程中遇到其他问题，欢迎在评论区留言，看到会第一时间回复！