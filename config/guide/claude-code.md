# Claude Code 接入 TierFlow 教程

本文介绍如何把 Claude Code 接入 TierFlow。

基础信息：

| 项目 | 值 |
|---|---|
| Base URL | `https://api.tierflow.ai/anthropic` |
| 认证方式 | Bearer Token |
| 兼容协议 | Anthropic API |
| Model | `claude code` |

## 1. 确认 Claude Code 已安装

Windows PowerShell：

```powershell
claude --version
```

macOS / Linux 终端：

```bash
claude --version
```

能看到版本号即可，例如：

```text
2.1.143 (Claude Code)
```

## 2. 配置文件位置

Claude Code 主要需要两个配置文件：

| 系统 | settings.json | .claude.json |
|---|---|---|
| Windows | `C:\Users\你的用户名\.claude\settings.json` | `C:\Users\你的用户名\.claude.json` |
| macOS | `/Users/你的用户名/.claude/settings.json` | `/Users/你的用户名/.claude.json` |
| Linux | `/home/你的用户名/.claude/settings.json` | `/home/你的用户名/.claude.json` |

## 3. 创建 `.claude` 文件夹

### Windows

打开文件资源管理器，在地址栏输入：

```text
%USERPROFILE%
```

在用户目录下创建文件夹：

```text
.claude
```

### macOS

打开终端：

```bash
mkdir -p ~/.claude
open ~/.claude
```

也可以在 Finder 里按 `Command + Shift + G`，输入：

```text
~/.claude
```

### Linux

打开终端：

```bash
mkdir -p ~/.claude
```

如果使用文件管理器，可以打开主目录，然后显示隐藏文件，再进入 `.claude`。

## 4. 创建 `settings.json`

在 `.claude` 文件夹里创建：

```text
settings.json
```

写入：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://api.tierflow.ai/anthropic",
    "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE",
    "ANTHROPIC_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude code"
  }
}
```

把：

```text
YOUR_API_KEY_HERE
```

替换成你的 API Key。

## 5. 创建 `.claude.json`

在用户目录创建：

```text
.claude.json
```

写入：

```json
{
  "hasCompletedOnboarding": true
}
```

对应位置：

Windows：

```text
C:\Users\你的用户名\.claude.json
```

macOS：

```text
/Users/你的用户名/.claude.json
```

Linux：

```text
/home/你的用户名/.claude.json
```

## 6. 重启终端

关闭当前终端，然后重新打开。

进入项目目录：

Windows PowerShell：

```powershell
cd C:\path\to\your\project
```

macOS / Linux：

```bash
cd /path/to/your/project
```

启动 Claude Code：

```bash
claude
```

第一次进入项目时，选择：

```text
Trust This Folder
```

## 7. 验证配置

在 Claude Code 里输入：

```text
/status
```

确认模型是：

```text
claude code
```

再测试一句：

```text
Reply exactly OK.
```

能正常返回内容就配置成功。

## 8. VS Code 插件配置

如果使用 Claude Code VS Code 插件，可以在 VS Code 的 `settings.json` 里配置：

```json
{
  "claudeCode.preferredLocation": "panel",
  "claudeCode.selectedModel": "claude code",
  "claudeCode.environmentVariables": [
    {
      "name": "ANTHROPIC_BASE_URL",
      "value": "https://api.tierflow.ai/anthropic"
    },
    {
      "name": "ANTHROPIC_AUTH_TOKEN",
      "value": "YOUR_API_KEY_HERE"
    },
    {
      "name": "ANTHROPIC_MODEL",
      "value": "claude code"
    },
    {
      "name": "ANTHROPIC_DEFAULT_SONNET_MODEL",
      "value": "claude code"
    },
    {
      "name": "ANTHROPIC_DEFAULT_OPUS_MODEL",
      "value": "claude code"
    },
    {
      "name": "ANTHROPIC_DEFAULT_HAIKU_MODEL",
      "value": "claude code"
    }
  ]
}
```

## 9. 常见问题

### 文件名不对

确认不是：

```text
settings.json.txt
.claude.json.txt
```

Windows 建议打开“显示文件扩展名”。

macOS / Linux 可以用：

```bash
ls -la ~/.claude ~/.claude.json
```

### 仍然走官方 Claude

检查是否设置过全局环境变量。

Windows PowerShell：

```powershell
echo $env:ANTHROPIC_BASE_URL
echo $env:ANTHROPIC_AUTH_TOKEN
```

macOS / Linux：

```bash
echo "$ANTHROPIC_BASE_URL"
echo "$ANTHROPIC_AUTH_TOKEN"
```

如果显示旧值，关闭并重新打开终端；如果 shell 配置文件里写过这些变量，需要删除旧配置。

### 认证失败

检查 `settings.json` 里：

```json
"ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE"
```

确认已经替换成真实 API Key。

### 配置改了但没生效

重启终端、VS Code、Cursor、Windows Terminal 等启动 Claude Code 的程序。

## 10. 可选：命令自动写入

如果你确认路径和 API Key 都没问题，可以用命令自动写入。

### Windows PowerShell

把 `YOUR_API_KEY_HERE` 换成你的 API Key：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude"

@'
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://api.tierflow.ai/anthropic",
    "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE",
    "ANTHROPIC_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude code"
  }
}
'@ | Set-Content -Encoding UTF8 "$env:USERPROFILE\.claude\settings.json"

@'
{
  "hasCompletedOnboarding": true
}
'@ | Set-Content -Encoding UTF8 "$env:USERPROFILE\.claude.json"
```

### macOS / Linux

把 `YOUR_API_KEY_HERE` 换成你的 API Key：

```bash
mkdir -p ~/.claude

cat > ~/.claude/settings.json <<'JSON'
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://api.tierflow.ai/anthropic",
    "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE",
    "ANTHROPIC_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude code",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude code"
  }
}
JSON

cat > ~/.claude.json <<'JSON'
{
  "hasCompletedOnboarding": true
}
JSON
```
