# Twitter CLI

[English](./README_EN.md) | 中文

一个专为 AI Agent 设计的 Twitter 命令行工具。所有输出均为结构化 JSON，方便程序解析和 LLM 消费。

## 功能

| 命令 | 说明 |
|------|------|
| `tweet <id_or_url>` | 获取推文详情（文本、媒体、互动数据、引用推文） |
| `user <screen_name>` | 获取用户资料（简介、头像、粉丝数等） |
| `user-tweets <screen_name>` | 获取用户推文列表（含置顶推文） |
| `search <query>` | 搜索推文 |
| `feed` | 获取首页时间线（For You） |

## 安装

从 [Releases](https://github.com/autoclaw-cc/twitter-cli/releases) 页面下载对应平台的二进制文件：

| 平台 | 文件 |
|------|------|
| macOS (Apple Silicon) | `twitter-cli-darwin-arm64` |
| macOS (Intel) | `twitter-cli-darwin-amd64` |
| Linux (x86_64) | `twitter-cli-linux-amd64` |

```bash
# 下载（以 macOS Apple Silicon 为例）
curl -L -o twitter-cli https://github.com/autoclaw-cc/twitter-cli/releases/latest/download/twitter-cli-darwin-arm64
chmod +x twitter-cli
sudo mv twitter-cli /usr/local/bin/
```

首次使用前，安装浏览器驱动：

```bash
twitter-cli install
```

## Cookie 认证

使用前需要配置 Twitter 登录态。支持两种方式：

**方式一：从浏览器自动导入（推荐）**

```bash
twitter-cli cookies import
```

自动从本地浏览器提取 Twitter cookie 并保存。

**方式二：手动从浏览器复制**

1. 打开浏览器，登录 [x.com](https://x.com)
2. 按 `F12` 打开开发者工具（DevTools）
3. 切换到 **Network**（网络）标签页
4. 刷新页面，随便点击一个 `x.com` 的请求
5. 在 **Request Headers** 中找到 `Cookie:` 一行，右键复制完整值
6. 运行：

```bash
twitter-cli cookies set "复制的完整 Cookie 值"
```

<!-- TODO: 后续补充截图 -->

验证 cookie 状态：

```bash
twitter-cli cookies status
```

## 使用示例

### 获取推文详情

```bash
# 通过推文 ID
twitter-cli tweet 1234567890

# 通过完整 URL
twitter-cli tweet https://x.com/jack/status/1234567890
```

### 获取用户资料

```bash
twitter-cli user elonmusk
twitter-cli user @jack    # 支持 @ 前缀
```

### 获取用户推文列表

```bash
twitter-cli user-tweets elonmusk
```

### 搜索推文

```bash
twitter-cli search "golang 2026"
```

### 获取首页时间线

```bash
twitter-cli feed
```

## 输出格式

所有命令统一输出 JSON：

**成功：**

```json
{
  "ok": true,
  "data": {
    "id": "1234567890",
    "text": "Hello, world!",
    "author": { "username": "jack", "name": "jack" },
    "created_at": "Mon Jan 01 00:00:00 +0000 2024",
    "stats": { "likes": 100, "retweets": 50, "replies": 10, "views": "1000" }
  }
}
```

**失败：**

```json
{
  "ok": false,
  "error": { "code": "auth_error", "message": "cookie expired" }
}
```

## 系统要求

- macOS 或 Linux
- 首次运行需要网络连接以安装浏览器驱动

## 许可证

[MIT License](./LICENSE)
