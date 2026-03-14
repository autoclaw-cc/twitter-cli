# Twitter CLI

English | [中文](./README.md)

A Twitter command-line tool designed for AI Agents. All output is structured JSON, making it easy for programs and LLMs to consume.

## Features

| Command | Description |
|---------|-------------|
| `tweet <id_or_url>` | Get tweet details (text, media, engagement, quoted tweets) |
| `user <screen_name>` | Get user profile (bio, avatar, follower count, etc.) |
| `user-tweets <screen_name>` | Get user's tweet list (including pinned tweet) |
| `search <query>` | Search tweets |
| `feed` | Get home timeline (For You) |

## Installation

Download the binary for your platform from the [Releases](https://github.com/autoclaw-cc/twitter-cli/releases) page:

| Platform | File |
|----------|------|
| macOS (Apple Silicon) | `twitter-cli-darwin-arm64` |
| macOS (Intel) | `twitter-cli-darwin-amd64` |
| Linux (x86_64) | `twitter-cli-linux-amd64` |

```bash
# Download (macOS Apple Silicon example)
curl -L -o twitter-cli https://github.com/autoclaw-cc/twitter-cli/releases/latest/download/twitter-cli-darwin-arm64
chmod +x twitter-cli
sudo mv twitter-cli /usr/local/bin/
```

Install the browser driver before first use:

```bash
twitter-cli install
```

## Cookie Authentication

You need to configure Twitter login credentials before use. Two methods are supported:

**Option 1: Auto-import from browser (Recommended)**

```bash
twitter-cli cookies import
```

Automatically extracts Twitter cookies from your local browser and saves them.

**Option 2: Manually copy from browser**

1. Open your browser and log in to [x.com](https://x.com)
2. Press `F12` to open Developer Tools (DevTools)
3. Switch to the **Application** tab
4. In the left sidebar, find **Cookies** → `https://x.com`
5. Find the `auth_token` and `ct0` cookies, copy their values
6. Run:

```bash
twitter-cli cookies set "auth_token=your_value; ct0=your_value"
```

<!-- TODO: Add screenshots later -->

Verify cookie status:

```bash
twitter-cli cookies status
```

## Usage Examples

### Get tweet details

```bash
# By tweet ID
twitter-cli tweet 1234567890

# By full URL
twitter-cli tweet https://x.com/jack/status/1234567890
```

### Get user profile

```bash
twitter-cli user elonmusk
twitter-cli user @jack    # @ prefix supported
```

### Get user tweets

```bash
twitter-cli user-tweets elonmusk
```

### Search tweets

```bash
twitter-cli search "golang 2026"
```

### Get home timeline

```bash
twitter-cli feed
```

## Output Format

All commands output JSON in a unified format:

**Success:**

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

**Error:**

```json
{
  "ok": false,
  "error": { "code": "auth_error", "message": "cookie expired" }
}
```

## System Requirements

- macOS or Linux
- Internet connection required on first run to install browser driver

## License

[MIT License](./LICENSE)
