---
title: WSL（Ubuntu）部署Nginx+PHP8.2完整教程（新手友好+避坑指南）
date: 2026-05-10 12:00:00
tags:
  - WSL
  - Ubuntu
  - Nginx
  - PHP8.2
  - 环境部署
categories:
  - 运维教程
description: 新手向WSL Ubuntu手把手部署Nginx+PHP8.2完整教程，全程避坑，从零搭建网站运行环境，适合零基础跟着操作。
---
# WSL（Ubuntu）部署Nginx\+PHP8\.2完整教程（新手友好\+避坑指南）

前言：WSL（Windows Subsystem for Linux）作为Windows下的轻量级Linux子系统，无需安装虚拟机即可搭建Linux开发环境，非常适合本地调试PHP\+Nginx项目。本文基于WSL2\+Ubuntu 22\.04，详细讲解Nginx安装、PHP8\.2安装、两者联动配置及常见问题排查，全程实操可复现，新手也能快速上手。

关键词：WSL2；Ubuntu；Nginx；PHP8\.2；部署教程；本地开发环境

## 一、环境准备（必做步骤）

### 1\.1 确认WSL版本及Ubuntu系统

首先确保你的WSL已升级至WSL2（WSL1兼容性较差，不推荐），且安装的是Ubuntu 20\.04及以上版本（本文以Ubuntu 22\.04为例，Ubuntu 20\.04操作基本一致）。

在Windows终端（PowerShell）中执行以下命令，查看WSL版本：

```bash
wsl --list --verbose  # 简写：wsl -l -v
```

若VERSION列显示1，需升级为WSL2，执行命令（替换Ubuntu\-22\.04为你的系统名称）：

```bash
wsl --set-version Ubuntu-22.04 2
```

升级完成后，重启WSL：

```bash
wsl --shutdown  # 关闭所有WSL子系统
wsl -d Ubuntu-22.04  # 启动目标Ubuntu系统
```

### 1\.2 更新Ubuntu软件源（提速关键）

默认Ubuntu软件源为国外源，下载速度较慢，建议替换为国内阿里云源，执行以下命令（全程sudo获取管理员权限）：

```bash
# 备份默认源（可选，建议备份）
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

# 替换为阿里云源（Ubuntu 22.04）
sudo sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list
sudo sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list

# 更新软件包列表和依赖
sudo apt update && sudo apt upgrade -y
```

更新完成后，后续安装软件速度会大幅提升，避免因网络问题导致安装失败。

## 二、部署Nginx（Web服务器）

### 2\.1 安装Nginx

Ubuntu系统可通过apt包管理器直接安装Nginx，无需源码编译（新手首选），执行命令：

```bash
sudo apt install nginx -y
```

安装完成后，查看Nginx版本，确认安装成功：

```bash
nginx -v  # 输出类似：nginx version: nginx/1.18.0 (Ubuntu)
```

### 2\.2 启动并设置Nginx开机自启

WSL默认不会自动启动系统服务，需手动启动Nginx，并设置开机自启（避免重启WSL后需重新启动）：

```bash
# 启动Nginx服务
sudo service nginx start

# 查看Nginx运行状态
sudo service nginx status

# 设置开机自启（关键：WSL重启后自动启动Nginx）
sudo systemctl enable nginx
```

状态显示“active \(running\)”即为启动成功。若启动失败，可执行`sudo nginx \-t`检查配置文件语法错误。

### 2\.3 验证Nginx是否可访问

两种验证方式，任选其一即可：

1. WSL内部验证：执行`curl localhost`，若输出Nginx默认欢迎页面的HTML代码，说明本地可访问；

2. Windows浏览器验证：打开浏览器，输入`http://localhost`，若看到“Welcome to nginx\!”页面，说明Nginx部署成功，且WSL与Windows网络互通。

补充：若浏览器无法访问，大概率是WSL防火墙限制，执行以下命令开放80端口（Nginx默认端口）：

```bash
sudo ufw allow 80/tcp  # 开放80端口
sudo ufw reload  # 重载防火墙配置
```

## 三、部署PHP8\.2（脚本解析器）

Ubuntu 22\.04默认PHP版本为8\.1，需手动添加PHP8\.2的官方源，再进行安装，避免安装旧版本。

### 3\.1 添加PHP8\.2官方源

```bash
# 安装依赖包（用于添加PPA源）
sudo apt install software-properties-common -y

# 添加PHP官方源（Ondrej sury，PHP官方维护者的PPA源）
sudo add-apt-repository ppa:ondrej/php -y

# 再次更新软件包列表，让系统识别新添加的PHP源
sudo apt update
```

### 3\.2 安装PHP8\.2及常用扩展

安装PHP8\.2核心组件及常用扩展（满足大部分PHP项目需求，如MySQL连接、文件上传等）：

```bash
sudo apt install php8.2 php8.2-fpm php8.2-mysql php8.2-cli php8.2-gd php8.2-curl php8.2-mbstring php8.2-xml php8.2-zip -y
```

各组件说明：

- php8\.2：PHP8\.2核心程序；

- php8\.2\-fpm：PHP FastCGI进程管理器，用于与Nginx联动（关键组件）；

- php8\.2\-mysql：PHP连接MySQL数据库的扩展；

- 其他扩展：gd（图片处理）、curl（网络请求）、mbstring（中文支持）等，按需安装。

### 3\.3 启动并设置PHP8\.2\-fpm开机自启

PHP8\.2\-fpm是Nginx解析PHP的核心，需确保其正常运行：

```bash
# 启动PHP8.2-fpm服务
sudo service php8.2-fpm start

# 查看运行状态
sudo service php8.2-fpm status

# 设置开机自启
sudo systemctl enable php8.2-fpm
```

状态显示“active \(running\)”即为启动成功。若启动失败，可查看日志排查：`sudo journalctl \-u php8\.2\-fpm`。

### 3\.4 验证PHP8\.2版本

```bash
php -v  # 输出类似：PHP 8.2.14 (cli) (built: Dec 21 2023 20:19:50) (NTS)
```

若输出PHP8\.2版本信息，说明安装成功。

## 四、关键配置：Nginx与PHP8\.2联动（核心步骤）

默认情况下，Nginx无法解析PHP文件，需修改Nginx配置文件，让Nginx将PHP请求转发给PHP8\.2\-fpm处理。

### 4\.1 备份Nginx默认配置文件

为避免配置错误无法恢复，先备份默认配置：

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default.bak
```

### 4\.2 修改Nginx配置文件

使用vim编辑Nginx默认配置文件（新手也可使用nano，命令：sudo nano /etc/nginx/sites\-available/default）：

```bash
sudo vim /etc/nginx/sites-available/default
```

找到以下配置段，修改并添加PHP解析相关配置（关键修改处已标注）：

```nginx
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    # 网站根目录（可自定义，本文使用默认目录）
    root /var/www/html;

    # 索引文件，添加index.php（优先解析PHP文件）
    index index.php index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        # 尝试查找请求的文件，找不到则返回404
        try_files $uri $uri/ =404;
    }

    # 新增PHP解析配置（关键）
    location ~ \.php$ {
        # 禁止访问php文件的目录遍历
        #try_files $uri =404;
        # 引入fastcgi配置片段
        include snippets/fastcgi-php.conf;
        # 指向PHP8.2-fpm的socket文件（路径需对应PHP版本）
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
    }

    # 禁止访问.htaccess文件（避免配置泄露）
    location ~ /\.ht {
        deny all;
    }
}
```

配置说明：

- index：添加index\.php，让Nginx优先解析PHP文件；

- location \~ \\\.php$：匹配所有以\.php结尾的请求，转发给PHP8\.2\-fpm处理；

- fastcgi\_pass：指定PHP8\.2\-fpm的socket路径，若路径错误会导致502错误，可通过`ls /var/run/php/`查看实际socket文件名。

### 4\.3 检查配置并重启服务

配置修改完成后，先检查Nginx配置语法是否正确：

```bash
sudo nginx -t
```

若输出“nginx: configuration file /etc/nginx/nginx\.conf test is successful”，说明配置无误，重启Nginx和PHP8\.2\-fpm服务，使配置生效：

```bash
sudo service nginx restart
sudo service php8.2-fpm restart
```

## 五、测试验证：确保PHP可正常解析

创建一个PHP测试文件，放在Nginx的网站根目录（/var/www/html），验证Nginx是否能正常解析PHP。

```bash
# 创建test.php文件
sudo vim /var/www/html/test.php
```

在文件中输入以下内容（PHP信息探针）：

```php
<?php
// 输出PHP环境信息
phpinfo();
?>
```

保存退出后，修改文件权限（避免权限不足导致无法访问）：

```bash
sudo chmod 755 /var/www/html/test.php
sudo chown www-data:www-data /var/www/html/test.php  # 与Nginx、PHP运行用户一致
```

验证方式：打开Windows浏览器，输入`http://localhost/test\.php`，若能看到PHP环境信息页面（包含PHP版本、扩展、服务器信息等），说明Nginx与PHP8\.2联动成功，部署完成！

注意：测试完成后，建议删除test\.php文件（避免泄露服务器敏感信息）：`sudo rm /var/www/html/test\.php`。

## 六、常见问题排查（新手必看）

### 问题1：浏览器访问localhost显示404

原因及解决：

- Nginx未启动：执行`sudo service nginx start`；

- 网站根目录错误：检查Nginx配置文件中root字段是否为/var/www/html，且该目录下有index\.html或index\.php文件；

- 防火墙限制：执行`sudo ufw allow 80/tcp`开放80端口。

### 问题2：访问test\.php显示502 Bad Gateway

原因及解决（最常见问题）：

- PHP8\.2\-fpm未启动：执行`sudo service php8\.2\-fpm start`；

- fastcgi\_pass路径错误：检查Nginx配置中fastcgi\_pass的socket路径，确保与`ls /var/run/php/`输出的socket文件名一致（如php8\.2\-fpm\.sock）；

- 权限不足：执行`sudo chown www\-data:www\-data /var/run/php/`，赋予PHP8\.2\-fpm socket文件正确权限。

### 问题3：访问test\.php显示PHP源码（未解析）

原因及解决：

- Nginx配置中未添加PHP解析规则：重新检查“四、关键配置”步骤，确保location \~ \\\.php$配置段正确；

- Nginx未重启：修改配置后需执行`sudo service nginx restart`。

### 问题4：WSL重启后，Nginx/PHP8\.2无法自动启动

原因：WSL默认不会自动启动systemd服务，需重新设置开机自启，执行：

```bash
sudo systemctl enable nginx
sudo systemctl enable php8.2-fpm
```

若仍无法自动启动，可在WSL启动时手动执行启动命令，或编写简易启动脚本。

## 七、总结

本文完整讲解了WSL（Ubuntu）环境下Nginx\+PHP8\.2的部署流程，核心步骤为：环境准备→Nginx安装→PHP8\.2安装→两者联动配置→测试验证。全程采用apt包管理器安装，无需源码编译，新手易操作，同时针对常见问题给出了具体排查方案。

部署完成后，你可以将PHP项目放在/var/www/html目录下，即可通过Windows浏览器访问，实现本地开发调试。后续可根据需求，继续部署MySQL、Redis等组件，搭建完整的LNMP开发环境。

如果本文对你有帮助，欢迎点赞、收藏，若有疑问或补充，欢迎在评论区留言\~

