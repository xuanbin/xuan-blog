---
title: Windows 系统 MinIO 完整安装部署详细教程（服务端+客户端+开机自启+常见坑）
date: 2026-05-10 17:33:42
tags:
  - MinIO
  - 对象存储
  - Windows
  - 教程
  - 部署
categories:
  - 软件教程
description: Windows 系统下 MinIO 对象存储服务的完整安装、配置、客户端使用、开机自启动设置及常见问题解决方案
---
# Windows 系统 MinIO 完整安装部署详细教程（服务端+客户端+开机自启+常见坑）
## 前言
MinIO 是基于 Go 语言开发的**轻量级高性能对象存储**，完全兼容 AWS S3 接口，常用来存放图片、文件、视频、附件等静态资源，是后端开发项目文件存储首选中间件。

Windows 环境下 MinIO 为**免安装绿色版**，无需解压、无需配置复杂环境，仅需下载二进制 exe 文件即可运行。本文从零完整讲解 Windows10/Windows11 下 MinIO 服务端部署、自定义账号密码、控制台访问、mc 客户端使用、开机后台自启、端口占用、访问失败等全部常见问题解决方案，开发测试环境直接可用。

## 一、环境准备
### 1.1 系统要求
- 操作系统：Windows 10、Windows 11、Windows Server 全系列 64 位系统
- 端口默认占用：`9000`（API 接口端口）、`9001`（Web 控制台端口）
- 权限：启动建议使用**管理员权限**，文件夹路径**不要包含中文、空格、特殊字符**

### 1.2 最新下载地址
#### 服务端 minio.exe
https://pan.quark.cn/s/710b26320cb4

#### 客户端 mc.exe（命令行工具）
https://pan.quark.cn/s/710b26320cb4

直接浏览器打开链接即可自动下载，无需注册登录。

## 二、目录结构创建
为了文件管理规范，统一规划文件夹，建议按照如下结构新建目录：
```
E:\MinIO
├─ bin          # 存放 minio.exe、mc.exe 可执行程序
├─ data         # MinIO 数据存储根目录（所有上传文件存放位置）
└─ logs         # 日志存放目录
```
将下载好的 `minio.exe`、`mc.exe` 放入 `bin` 文件夹内。

## 三、自定义账号密码配置
MinIO 默认账号密码：
```
账号：minioadmin
密码：minioadmin
```
默认账号安全性低，**强烈建议自定义管理员账号密码**。

### 方式1：临时窗口配置（当前cmd生效）
打开 **管理员模式 CMD**，依次执行：
```cmd
set MINIO_ROOT_USER=admin
set MINIO_ROOT_PASSWORD=Admin@123456
```

### 方式2：系统永久环境变量（全局生效）
1. 此电脑右键 → 属性 → 高级系统设置 → 环境变量
2. 系统变量 → 新建
```
变量名：MINIO_ROOT_USER
变量值：admin
```
3. 再次新建
```
变量名：MINIO_ROOT_PASSWORD
变量值：Admin@123456
```
全部保存确定，**重新打开CMD**即可永久生效。

## 四、MinIO 服务端启动
### 4.1 命令行临时启动（测试用）
进入 `E:\MinIO\bin` 目录，在地址栏输入 `cmd` 回车直接打开命令窗口，执行启动命令：
```cmd
minio.exe server E:\MinIO\data --console-address :9001
```

**命令参数说明**
- `E:\MinIO\data`：数据存储本地路径
- `--console-address :9001`：Web 管理控制台访问端口
- 默认 API 端口：`9000`

启动成功控制台输出：
```
API: http://127.0.0.1:9000 http://本机IP:9000
RootUser: admin
RootPass: Admin@123456
Console: http://127.0.0.1:9001 http://本机IP:9001
```

浏览器访问控制台：
```
http://127.0.0.1:9001
```
输入自定义账号密码即可登录后台。

> 缺点：关闭CMD窗口，服务直接停止。

### 4.2 bat 脚本后台常驻启动（推荐）
在 `E:\MinIO` 目录新建 `start-minio.bat` 批处理脚本，内容如下：
```bat
@echo off
title MinIO对象存储服务
set MINIO_ROOT_USER=admin
set MINIO_ROOT_PASSWORD=Admin@123456
cd /d E:\MinIO\bin
start /b minio.exe server E:\MinIO\data --console-address :9001 > E:\MinIO\logs\minio.log 2>&1
echo ==============================================
echo          MinIO 服务后台启动成功！
echo  控制台访问地址：http://127.0.0.1:9001
echo  接口地址：http://127.0.0.1:9000
echo  日志目录：E:\MinIO\logs\minio.log
echo ==============================================
pause
```
**右键以管理员身份运行**此脚本，服务后台运行，关闭窗口不停止服务。

## 五、修改默认端口（端口占用解决方案）
如果 9000、9001 被其他程序占用，自定义端口启动，示例修改为 9005、9006：
```cmd
minio.exe server E:\MinIO\data --address :9005 --console-address :9006
```
- `--address :9005` 修改接口API端口
- `--console-address :9006` 修改网页控制台端口

## 六、MinIO 客户端 mc 安装与使用
mc 是 MinIO 官方命令行客户端，用于创建桶、上传下载文件、权限管理等操作。
### 6.1 配置环境变量（可选）
把 `E:\MinIO\bin` 路径添加到系统 `Path` 环境变量，全局任意位置可调用 mc 命令。

验证版本：
```cmd
mc --version
```

### 6.2 连接本地 MinIO 服务
```cmd
mc alias set myminio http://127.0.0.1:9000 admin Admin@123456
```
参数说明：
- `myminio` 自定义别名
- 后面依次为：服务地址、账号、密码

### 6.3 常用 mc 命令大全
| 操作 | 命令 | 说明 |
| ---- | ---- | ---- |
| 查看服务信息 | `mc admin info myminio` | 查看服务状态、存储空间 |
| 创建存储桶 | `mc mb myminio/testbucket` | 桶名必须小写英文 |
| 查看所有桶 | `mc ls myminio` | 列出所有存储桶 |
| 上传文件 | `mc cp D:\test.jpg myminio/testbucket/` | 本地文件上传 |
| 下载文件 | `mc cp myminio/testbucket/test.jpg D:\` | 桶内文件下载本地 |
| 删除文件 | `mc rm myminio/testbucket/test.jpg` | 删除桶内文件 |
| 删除存储桶 | `mc rb --force myminio/testbucket` | 强制删除非空桶 |

## 七、Windows 开机自启配置（完美方案）
实现电脑开机自动启动 MinIO，无需手动双击脚本。
1. 按下 `Win + R` 输入 `shell:startup` 打开**开机启动文件夹**
2. 右键 `start-minio.bat` 脚本，创建**快捷方式**
3. 将快捷方式放入打开的启动文件夹内
4. 重启电脑测试，服务自动后台运行

## 八、常见问题与踩坑汇总
### 问题1：双击 minio.exe 黑窗口一闪而过
**原因**：MinIO 不支持直接双击运行，必须携带数据目录参数启动。
**解决**：通过 CMD 命令启动，或使用编写好的 bat 脚本启动。

### 问题2：端口 9000/9001 被占用
查看端口占用进程：
```cmd
netstat -ano | findstr "9000"
netstat -ano | findstr "9001"
```
解决方式：
1. 任务管理器结束对应占用进程
2. 启动命令自定义更换端口号

### 问题3：浏览器无法访问 http://127.0.0.1:9001
1. 检查 minio.exe 进程是否正在运行
2. 检查地址、端口号是否与启动命令一致
3. 关闭系统防火墙、第三方安全软件拦截
4. 确认路径无中文、无空格

### 问题4：账号密码登录失败
1. 环境变量未刷新，**关闭所有CMD重新打开**
2. 密码大小写、特殊字符输入错误
3. 新版本 MinIO 废弃旧版 `MINIO_ACCESS_KEY`，统一使用 `MINIO_ROOT_USER`

### 问题5：路径包含中文导致启动异常
MinIO 不兼容中文路径、空格路径，所有目录必须纯英文。

## 九、总结
1. Windows 仅适合**开发测试环境**部署 MinIO，生产环境推荐 Linux 服务器分布式部署
2. 目录路径务必纯英文，禁止中文、空格
3. 自定义账号密码，不要使用默认 minioadmin 账号
4. 后台启动使用 bat 脚本，配合开机自启满足项目本地开发文件存储需求
5. 完全兼容 S3 协议，后端 Java/SpringBoot 项目直接对接无适配问题

> 原创不易，点赞收藏不迷路，如有部署问题可评论区留言。