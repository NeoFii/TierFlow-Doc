# Claude Code TierFlow Setup

This guide shows how to connect Claude Code to TierFlow.

Basic information:

| Item | Value |
|---|---|
| Base URL | `https://cn.tierflow.ai` |
| Authentication | Bearer Token |
| Protocol | Anthropic API Compatible |
| Model | `claude` |

## 1. Check That Claude Code Is Installed

Windows PowerShell:

```powershell
claude --version
```

macOS / Linux terminal:

```bash
claude --version
```

If a version number is shown, Claude Code is installed. For example:

```text
2.1.143 (Claude Code)
```

## 2. Config File Locations

Claude Code mainly uses two config files:

| System | settings.json | .claude.json |
|---|---|---|
| Windows | `C:\Users\YOUR_USERNAME\.claude\settings.json` | `C:\Users\YOUR_USERNAME\.claude.json` |
| macOS | `/Users/YOUR_USERNAME/.claude/settings.json` | `/Users/YOUR_USERNAME/.claude.json` |
| Linux | `/home/YOUR_USERNAME/.claude/settings.json` | `/home/YOUR_USERNAME/.claude.json` |

## 3. Create the `.claude` Folder

### Windows

Open File Explorer and enter this in the address bar:

```text
%USERPROFILE%
```

Create this folder under your user directory:

```text
.claude
```

### macOS

Open Terminal:

```bash
mkdir -p ~/.claude
open ~/.claude
```

You can also open Finder, press `Command + Shift + G`, and enter:

```text
~/.claude
```

### Linux

Open Terminal:

```bash
mkdir -p ~/.claude
```

If you use a file manager, open your home directory, show hidden files, then enter `.claude`.

## 4. Create `settings.json`

Create this file inside the `.claude` folder:

```text
settings.json
```

Write:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://cn.tierflow.ai",
    "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE",
    "ANTHROPIC_MODEL": "claude",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude"
  }
}
```

Replace:

```text
YOUR_API_KEY_HERE
```

with your real API key.

## 5. Create `.claude.json`

Create this file in your user directory:

```text
.claude.json
```

Write:

```json
{
  "hasCompletedOnboarding": true
}
```

File locations:

Windows:

```text
C:\Users\YOUR_USERNAME\.claude.json
```

macOS:

```text
/Users/YOUR_USERNAME/.claude.json
```

Linux:

```text
/home/YOUR_USERNAME/.claude.json
```

## 6. Restart the Terminal

Close the current terminal and open it again.

Enter your project directory:

Windows PowerShell:

```powershell
cd C:\path\to\your\project
```

macOS / Linux:

```bash
cd /path/to/your/project
```

Start Claude Code:

```bash
claude
```

When entering a project for the first time, select:

```text
Trust This Folder
```

## 7. Verify the Setup

In Claude Code, type:

```text
/status
```

Confirm the model is:

```text
claude
```

Then test with:

```text
Reply exactly OK.
```

If Claude Code returns a normal response, the setup is complete.

## 8. VS Code Extension Setup

If you use the Claude Code VS Code extension, configure VS Code `settings.json` like this:

```json
{
  "claudeCode.preferredLocation": "panel",
  "claudeCode.selectedModel": "claude",
  "claudeCode.environmentVariables": [
    {
      "name": "ANTHROPIC_BASE_URL",
      "value": "https://cn.tierflow.ai"
    },
    {
      "name": "ANTHROPIC_AUTH_TOKEN",
      "value": "YOUR_API_KEY_HERE"
    },
    {
      "name": "ANTHROPIC_MODEL",
      "value": "claude"
    },
    {
      "name": "ANTHROPIC_DEFAULT_SONNET_MODEL",
      "value": "claude"
    },
    {
      "name": "ANTHROPIC_DEFAULT_OPUS_MODEL",
      "value": "claude"
    },
    {
      "name": "ANTHROPIC_DEFAULT_HAIKU_MODEL",
      "value": "claude"
    }
  ]
}
```

## 9. Troubleshooting

### Wrong File Name

Make sure the files are not named:

```text
settings.json.txt
.claude.json.txt
```

On Windows, enable file extension display.

On macOS / Linux, you can check with:

```bash
ls -la ~/.claude ~/.claude.json
```

### Claude Code Still Uses Official Claude

Check whether old global environment variables are set.

Windows PowerShell:

```powershell
echo $env:ANTHROPIC_BASE_URL
echo $env:ANTHROPIC_AUTH_TOKEN
```

macOS / Linux:

```bash
echo "$ANTHROPIC_BASE_URL"
echo "$ANTHROPIC_AUTH_TOKEN"
```

If old values are shown, close and reopen the terminal. If these variables were written into a shell config file, remove the old config there.

### Authentication Failed

Check this value in `settings.json`:

```json
"ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE"
```

Make sure it has been replaced with your real API key.

### Config Changed but Did Not Take Effect

Restart the terminal, VS Code, Cursor, Windows Terminal, or whichever program starts Claude Code.

## 10. Optional Command Write

Use this only if you have confirmed the paths and API key. Manual editing is safer for new users.

### Windows PowerShell

Replace `YOUR_API_KEY_HERE` with your API key:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude"

@'
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://cn.tierflow.ai",
    "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE",
    "ANTHROPIC_MODEL": "claude",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude"
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

Replace `YOUR_API_KEY_HERE` with your API key:

```bash
mkdir -p ~/.claude

cat > ~/.claude/settings.json <<'JSON'
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://cn.tierflow.ai",
    "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY_HERE",
    "ANTHROPIC_MODEL": "claude",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude"
  }
}
JSON

cat > ~/.claude.json <<'JSON'
{
  "hasCompletedOnboarding": true
}
JSON
```
