---
title: Claude Code 免费接入 NVIDIA NIM 国产大模型完整教程（零成本可用）
date: 2026-05-10 17:50:51
tags:
  - Claude Code
  - NVIDIA NIM
  - 国产大模型
  - CLIProxyAPI
  - 反向代理
  - AI编程
categories:
  - AI工具
description: Claude Code 免费接入 NVIDIA NIM 国产大模型的完整配置教程,实现零成本使用国产大模型进行代码辅助开发
---

## 前言

Claude Code 作为终端 AI 编程利器，官方 API 成本较高，而 NVIDIA NIM 平台免费开放 GLM-4.7、MiniMax M2.5、Kimi K2.5 等国产优质模型，可满足代码生成、调试、长上下文理解等需求。

**核心问题**：NVIDIA API 为 OpenAI 兼容协议，Claude Code 要求 Anthropic 协议，无法直连。

**解决方案**：用 CLIProxyAPI 做反向代理实现协议转换，全程免费、10 分钟即可配置完成，OpenClaw 等工具可复用此思路。

---

## 一、申请 NVIDIA API Key（必做第一步）

### 1.1 注册 NVIDIA 开发者账号

打开官网：<https://build.nvidia.com/>，完成注册登录（支持邮箱、谷歌账号等方式，流程简单无门槛）。

### 1.2 手机号验证（国内用户必看）

注册后进入 Verify 验证页面，**手机号必须加 +86 区号**，格式：`+86138xxxxxxxx`（例：`+8613800138000`），否则会直接验证失败，无法继续操作。

### 1.3 生成并保存 API Key

1. 点击页面右上角头像，选择「API Keys」；
2. 点击「Generate API Key」，生成专属 API Key；
3. ⚠️ **关键提醒**：Key 仅显示一次，生成后立即复制，保存到记事本或备忘录，后续配置会反复用到，丢失需重新生成。

---

## 二、部署 CLIProxyAPI 反向代理（协议转换核心）

### 2.1 下载 CLIProxyAPI

前往下载对应系统版本：<https://pan.quark.cn/s/cb89d172c72c>

- **Windows 系统**：选择 `windows_amd64.zip` 压缩包
- **其他系统**（Mac、Linux）：选择对应架构的压缩包

下载后解压到本地任意目录（建议路径无中文、无空格，例：`D:\CLIProxyAPI`）。

### 2.2 编辑配置文件

1. 进入解压后的文件夹，找到 `config.example.yaml` 文件；
2. 复制该文件，重命名为 `config.yaml`（**必须是这个名称**，否则代理无法启动）；
3. 用记事本、VS Code 等工具打开 `config.yaml`，修改以下 3 个关键配置（其他参数保持默认即可）：

```yaml
# 管理后台密码，自行设置（建议复杂一点，避免泄露）
secret-key: "你的后台密码"

# 允许远程访问（默认false，改为true，方便后续配置）
allow-remote: true

# 填入刚才申请的 NVIDIA API Key（完整复制，不要遗漏字符）
api-keys: "nvapi-xxxxxx"
```

### 2.3 启动代理服务

**Windows 系统**：双击打开解压目录中的 `cli-proxy-api.exe`，启动后会弹出命令行窗口，显示 `Listening on :8317` 即启动成功。

⚠️ **注意**：启动后的命令行窗口**不能关闭**，关闭则代理服务停止，后续 Claude Code 无法连接。

### 2.4 后台添加 AI 提供商

1. 打开浏览器，访问地址：<http://localhost:8317/management.html>
2. 输入刚才在 `config.yaml` 中设置的 `secret-key`，登录管理后台；
3. 左侧导航栏选择「AI 提供商」→ 点击「添加提供商」；
4. 填写以下信息（严格按照要求填写，否则无法连通）：

   | 配置项 | 填写内容 |
   |--------|----------|
   | 提供商名称 | `nvidia`（小写，不能修改） |
   | Base URL | `https://integrate.api.nvidia.com/v1`（完整复制，不要多空格） |
   | API 密钥 | 填入第一步申请的 NVIDIA API Key |
   | 模型列表 | 点击「添加模型」，输入 `z-ai/glm4.7`（推荐，稳定不易报错） |

5. 点击「保存」，系统会自动测试连通性，显示"连通成功"即可进入下一步。

---

## 三、配置 Claude Code 连接代理（两种方式任选）

### 方式一：CC Switch 工具（推荐，可视化管理，小白友好）

1. 打开 CC Switch 工具（Claude Code 常用辅助工具，自行安装）；
2. 点击「新建供应商」，填写以下关键参数：

   - **API Key**：填入 NVIDIA API Key
   - **请求地址**：`http://localhost:8317`（与代理服务端口一致）
   - **API 格式**：选择「Anthropic Messages (原生)」
   - **主模型**：选择 `z-ai/glm4.7`

3. 点击「保存」，并点击「应用配置」，配置立即生效。

### 方式二：手动修改配置文件（无额外工具，适合有基础的用户）

1. 找到 Claude Code 配置目录：默认路径为 `~/.claude/settings.json`（Windows 可通过"运行"输入 `%USERPROFILE%/.claude` 快速找到）；
2. 用编辑工具打开 `settings.json`，写入以下配置（二选一即可）：

#### 配置方式1（基础写法）

```json
{
  "apiBaseUrl": "http://localhost:8317",
  "apiKey": "你的 NVIDIA API Key"
}
```

#### 配置方式2（环境变量写法，更稳定）

```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "nvapi-xxxx",
    "ANTHROPIC_BASE_URL": "http://localhost:8317",
    "ANTHROPIC_MODEL": "z-ai/glm4.7"
  }
}
```

3. 保存文件后，重启终端（关闭所有 Claude Code 相关窗口，重新打开），配置生效。

---

## 四、验证与可用模型清单

### 4.1 验证是否成功

1. 打开终端，输入命令：

```bash
claude
```

2. 终端提示输入内容后，输入「你是哪个模型」，回车；
3. 若返回「我是 z-ai/glm4.7 模型」，则说明配置成功，可正常使用；若提示报错，参考第五部分常见问题排查。

### 4.2 免费可用模型（NVIDIA NIM 平台）

| 模型标识 | 模型名称 | 核心优势 |
|----------|----------|----------|
| `z-ai/glm4.7` | GLM-4.7 | 数学推理强，稳定可靠，优先推荐使用 |
| `z-ai/glm5` | GLM-5 | 综合能力更强，支持更复杂的编程需求 |
| `minimaxai/minimax-m2.5` | MiniMax M2.5 | 代码编辑、bug 修复能力优秀，适合开发场景 |
| `moonshotai/kimi-k2.5` | Kimi K2.5 | 长上下文支持极佳，可处理大段代码、文档解析 |

💡 **提示**：GLM-5、MiniMax M2.7 偶有不稳定（受 NVIDIA 服务器波动影响），日常使用优先选择 GLM-4.7，稳定性最佳。

---

## 五、常见问题与避坑指南

### ❓ 问题1：手机号验证失败

**解决方法**：必须加 `+86` 区号，格式严格按照 `+86138xxxxxxxx`，不要添加空格、括号。

### ❓ 问题2：代理无法启动

**解决方法**：
1. 检查 8317 端口是否被其他程序占用（可通过"任务管理器"关闭占用端口的程序）
2. 或重新解压 CLIProxyAPI 重试

### ❓ 问题3：Claude Code 连接失败

**解决方法**：
1. 确认 CLIProxyAPI 命令行窗口未关闭
2. `config.yaml` 中 `allow-remote` 设为 `true`
3. 请求地址填写正确

### ❓ 问题4：模型调用报错

**解决方法**：
1. 切换为 GLM-4.7 重试
2. 若仍报错，检查 NVIDIA API Key 是否正确
3. 或重启代理服务

### ❓ 问题5：权限问题

**解决方法**：Windows 系统若提示"权限不足"，右键点击 `cli-proxy-api.exe`，选择「以管理员身份运行」。

---

## 总结

本方案通过 **NVIDIA 免费 API + CLIProxyAPI 协议转换**，实现 Claude Code 零成本调用国产大模型，兼顾性能与成本，适合日常开发、学习使用。

✅ **配置简单、稳定性高**，无需复杂技术储备，10 分钟即可完成部署，是 Claude Code 官方 API 的高性价比平替方案。

如果配置过程中遇到其他问题，可在评论区留言，看到后会及时回复排查！

 **点赞+收藏**，后续查看更方便～
