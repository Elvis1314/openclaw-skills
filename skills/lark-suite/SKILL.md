---
name: lark-suite
description: |
  飞书/Lark 开放平台命令行工具（lark-cli）。覆盖消息、文档、多维表格、电子表格、日历、邮箱、任务、会议等核心业务域，提供 200+ 命令及 19 个 AI Agent Skills。
  触发场景：用户提到飞书、lark、larksuite、lark-cli、飞书文档、飞书日历、飞书消息、飞书任务、飞书多维表格、飞书表格、飞书邮箱、飞书会议、飞书知识库时使用此技能。
homepage: https://github.com/larksuite/cli
version: 1.0.0
author: openclaw-community
metadata:
  openclaw:
    emoji: "🐦"
    category: "messaging"
    requires:
      bins:
        - lark-cli
---

# 飞书/Lark 命令行工具 (lark-cli)

通过 `lark-cli` 操作飞书开放平台的全部核心功能。

## 安装

本技能已安装 `lark-cli`，二进制文件位于：

```
C:\Users\admin\.lark-cli\lark-cli.exe
```

> **注意**：新版终端会话中可直接使用 `lark-cli` 命令（已加入用户 PATH）。
> 当前会话中请使用完整路径：`& "C:\Users\admin\.lark-cli\lark-cli.exe"`

### 手动重装（如需更新）

```bash
npm install -g @larksuite/cli
# 或从 GitHub Releases 手动下载: https://github.com/larksuite/cli/releases
```

### 验证安装

```bash
& "C:\Users\admin\.lark-cli\lark-cli.exe" --version
```

## 认证配置（首次使用必须）

### 第 1 步：配置应用凭证

```bash
lark-cli config init --new
```

此命令会输出一个授权 URL。**将此 URL 发送给用户**，用户在浏览器中完成飞书开放平台应用创建和配置后，命令会自动退出。

### 第 2 步：登录授权

```bash
lark-cli auth login --recommend
```

同样会输出授权 URL，用户在浏览器中完成授权。

### 第 3 步：验证

```bash
lark-cli auth status
```

## 三层命令架构

| 层级 | 说明 | 示例 |
|------|------|------|
| 快捷命令 | 人机友好，最常用场景 | `lark-cli calendar +agenda` |
| API 命令 | 平台同步，完整参数 | `lark-cli calendar list-events` |
| 通用调用 | 全 API 覆盖 | `lark-cli api post /open-apis/calendar/v4/calendars` |

## 核心命令速查

### 📅 日历 (calendar)

```bash
lark-cli calendar +agenda              # 查看今日日程
lark-cli calendar list-events           # 列出日程
lark-cli calendar create-event          # 创建日程
lark-cli calendar freebusy              # 查询忙闲
lark-cli calendar time-suggest          # 时间建议
```

### 💬 即时通讯 (im)

```bash
lark-cli im send-message                # 发送消息
lark-cli im reply-message               # 回复消息
lark-cli im list-chats                  # 列出群聊
lark-cli im search-messages             # 搜索消息
lark-cli im upload-image                # 上传图片
lark-cli im upload-file                 # 上传文件
```

### 📄 云文档 (doc)

```bash
lark-cli doc create                     # 创建文档
lark-cli doc read                       # 读取文档
lark-cli doc update                     # 更新文档（基于 Markdown）
lark-cli doc search                     # 搜索文档
```

### 📁 云空间 (drive)

```bash
lark-cli drive upload                   # 上传文件
lark-cli drive download                 # 下载文件
lark-cli drive search                   # 搜索文件
```

### 📊 多维表格 (base)

```bash
lark-cli base list-tables               # 列出多维表格
lark-cli base list-records              # 列出记录
lark-cli base create-record             # 创建记录
lark-cli base update-record             # 更新记录
lark-cli base list-fields               # 列出字段
```

### 📈 电子表格 (sheets)

```bash
lark-cli sheets create                  # 创建表格
lark-cli sheets read                    # 读取表格
lark-cli sheets write                   # 写入表格
lark-cli sheets append                  # 追加数据
lark-cli sheets find                    # 查找数据
lark-cli sheets export                  # 导出表格
```

### ✅ 任务 (task)

```bash
lark-cli task create                    # 创建任务
lark-cli task list                      # 列出任务
lark-cli task update                    # 更新任务
lark-cli task complete                  # 完成任务
```

### 📚 知识库 (wiki)

```bash
lark-cli wiki create-space              # 创建知识空间
lark-cli wiki list-nodes                # 列出节点
lark-cli wiki create-node               # 创建节点
```

### 👤 通讯录 (contact)

```bash
lark-cli contact search                 # 搜索用户
lark-cli contact get-user               # 获取用户信息
```

### 📧 邮箱 (mail)

```bash
lark-cli mail list                      # 列出邮件
lark-cli mail read                      # 读取邮件
lark-cli mail send                      # 发送邮件
lark-cli mail reply                     # 回复邮件
lark-cli mail search                    # 搜索邮件
```

### 🎥 会议 (vc)

```bash
lark-cli vc search-meetings             # 搜索会议记录
lark-cli vc minutes                     # 会议纪要产物
```

## 常见问题

### 安装失败 ETIMEDOUT
npm 安装时需要从 GitHub 下载预编译二进制，网络不通时超时。解决方案：
1. 配置 npm 代理
2. 手动从 GitHub Releases 下载二进制放到 PATH

### 认证过期
重新执行 `lark-cli auth login --recommend` 即可。

### 权限不足
使用 `lark-cli auth login` 并选择所需权限范围，或通过 `lark-cli config init` 重新配置应用。

## 安全提示

- 凭证存储在 OS 原生密钥链中
- 命令内置输入防注入和输出净化
- 切勿在命令行中明文传递敏感信息
