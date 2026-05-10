---
title: 常用命令手册
date: 2026-05-10 20:48:00
---

# 博客项目常用命令手册

本文档记录了博客项目日常使用的各种命令，方便快速查阅。

---

## 📦 Hexo 基础命令

### 服务器相关

```bash
# 启动本地开发服务器（默认端口 4000）
npx hexo server
# 或简写
npx hexo s

# 指定端口启动
npx hexo s -p 5000

# 指定 IP 地址启动
npx hexo s -i 192.168.1.100
```

### 生成与部署

```bash
# 清理缓存和生成的静态文件
npx hexo clean

# 生成静态文件
npx hexo generate
# 或简写
npx hexo g

# 部署到远程仓库
npx hexo deploy
# 或简写
npx hexo d

# 一键清理、生成、部署
hexo clean && hexo g && hexo d
```

### 文章管理

```bash
# 创建新文章
npx hexo new "文章标题"

# 创建新页面
npx hexo new page "页面名称"

# 创建草稿
npx hexo new draft "草稿标题"

# 发布草稿
npx hexo publish "草稿标题"
```

---

## 🔧 Git 常用命令

### 基础操作

```bash
# 查看当前状态
git status

# 添加所有变更到暂存区
git add .

# 添加指定文件
git add 文件名

# 提交变更
git commit -m "提交信息"

# 推送到远程仓库
git push

# 拉取远程更新
git pull
```

### 查看与对比

```bash
# 查看提交历史
git log

# 查看简洁的提交历史
git log --oneline

# 查看最近的 5 条提交
git log -5

# 查看变更内容
git diff

# 查看暂存区的变更
git diff --staged
```

### 分支管理

```bash
# 查看所有分支
git branch

# 创建新分支
git branch 分支名

# 切换分支
git checkout 分支名

# 创建并切换分支
git checkout -b 分支名

# 删除分支
git branch -d 分支名
```

### 远程仓库

```bash
# 查看远程仓库地址
git remote -v

# 添加远程仓库
git remote add origin 仓库地址

# 修改远程仓库地址
git remote set-url origin 新地址

# 查看本地分支与远程分支的关联
git branch -vv
```

---

## 🌐 网络与代理配置

### Git 代理设置

```bash
# 配置 HTTP 代理
git config --global http.proxy http://127.0.0.1:7890

# 配置 HTTPS 代理
git config --global https.proxy http://127.0.0.1:7890

# 取消 HTTP 代理
git config --global --unset http.proxy

# 取消 HTTPS 代理
git config --global --unset https.proxy

# 查看当前代理配置
git config --global --get http.proxy
git config --global --get https.proxy
```

### SSL 证书验证

```bash
# 禁用 SSL 证书验证（临时解决连接问题）
git config --global http.sslVerify false

# 恢复 SSL 证书验证
git config --global http.sslVerify true
```

---

## 🔍 问题排查命令

### 端口占用检查

```bash
# 查看端口占用（Windows）
netstat -ano | findstr :4000

# 强制终止占用端口的进程（PID 替换为实际进程号）
taskkill /F /PID 12345
```

### Git 连接测试

```bash
# 测试 GitHub SSH 连接
ssh -T git@github.com

# 测试 HTTPS 连接
git ls-remote https://github.com/用户名/仓库名.git
```

---

## 📁 文件系统操作

### 文件查看

```bash
# 查看文件内容（Windows PowerShell）
cat 文件名

# 查看文件前 10 行
head -n 10 文件名

# 查看文件后 10 行
tail -n 10 文件名

# 统计文件行数
wc -l 文件名
```

### 目录操作

```bash
# 列出当前目录内容
ls
# 或
dir

# 列出详细信息
ls -l

# 列出隐藏文件
ls -a

# 切换目录
cd 目录路径

# 返回上级目录
cd ..

# 返回根目录
cd /
```

---

## ️ npm 相关命令

### 包管理

```bash
# 安装依赖
npm install
# 或简写
npm i

# 安装指定包
npm install 包名

# 卸载包
npm uninstall 包名

# 更新包
npm update 包名

# 安装全局包
npm install -g 包名
```

### 项目脚本

```bash
# 运行 build 脚本
npm run build

# 运行 server 脚本
npm run server

# 运行 clean 脚本
npm run clean

# 运行 deploy 脚本
npm run deploy
```

### 缓存管理

```bash
# 清理 npm 缓存
npm cache clean --force

# 查看 npm 缓存
npm cache ls
```

---

## 🔐 SSH 密钥管理

### 生成与配置

```bash
# 生成 SSH 密钥（默认 RSA）
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# 生成 ED25519 密钥（推荐）
ssh-keygen -t ed25519 -C "your_email@example.com"

# 查看公钥
cat ~/.ssh/id_rsa.pub
# 或
cat ~/.ssh/id_ed25519.pub

# 添加 SSH 密钥到 ssh-agent
ssh-add ~/.ssh/id_rsa
```

### 测试连接

```bash
# 测试 GitHub SSH 连接
ssh -T git@github.com

# 测试 GitLab SSH 连接
ssh -T git@gitlab.com
```

---

## 📝 Markdown 快捷语法

### 标题

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
```

### 文本格式

```markdown
**粗体文本**
*斜体文本*
~~删除线~~
`行内代码`
```

### 列表

```markdown
- 无序列表项 1
- 无序列表项 2

1. 有序列表项 1
2. 有序列表项 2
```

### 链接与图片

```markdown
[链接文字](https://example.com)
![图片描述](图片路径)
```

### 代码块

````markdown
```javascript
const code = "示例代码";
console.log(code);
```
````

### 表格

```markdown
| 列1 | 列2 | 列3 |
|-----|-----|-----|
| 内容1 | 内容2 | 内容3 |
```

---

##  快速部署流程

### 完整部署步骤

```bash
# 1. 清理缓存
npx hexo clean

# 2. 生成静态文件
npx hexo generate

# 3. 部署到远程
npx hexo deploy

# 或者一键完成
npx hexo clean && npx hexo generate && npx hexo deploy
```

### 本地预览

```bash
# 启动本地服务器
npx hexo server

# 访问地址
http://localhost:4000
```

---

##  常见问题命令

### 端口被占用

```bash
# 1. 查找占用端口的进程
netstat -ano | findstr :4000

# 2. 终止进程（替换 PID）
taskkill /F /PID <进程号>

# 3. 重新启动服务器
npx hexo server
```

### Git 推送失败

```bash
# 1. 检查网络连接
ping github.com

# 2. 查看远程仓库配置
git remote -v

# 3. 尝试重新推送
git push

# 4. 如果还是失败，尝试拉取最新代码
git pull --rebase
git push
```

### SSL 连接问题

```bash
# 临时禁用 SSL 验证
git config --global http.sslVerify false

# 完成部署后恢复
git config --global http.sslVerify true
```

---

## 💡 实用技巧

### Git 别名配置

```bash
# 配置常用别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --all"
```

### Hexo 配置检查

```bash
# 验证配置文件
npx hexo config

# 查看特定配置项
npx hexo config title
```

---

## 📚 参考资源

- **Hexo 官方文档**: https://hexo.io/zh-cn/docs/
- **Git 官方文档**: https://git-scm.com/doc
- **Markdown 语法**: https://www.markdownguide.org/
- **GitHub 帮助**: https://docs.github.com/

---

> 💡 **提示**: 本手册会随着项目发展持续更新，欢迎补充更多实用命令！