# CC Switch TierFlow Setup

This guide explains how to use CC Switch to manage TierFlow settings for Claude Code and Codex.

CC Switch is a cross-platform desktop app for managing provider settings across AI coding tools such as Claude Code, Codex, OpenCode, OpenClaw, and Gemini CLI. With CC Switch, you can switch providers from a UI instead of repeatedly editing `settings.json`, `auth.json`, and `config.toml`.

Basic information:

| Tool | Protocol | Base URL | Model |
|---|---|---|---|
| Claude Code | Anthropic API Compatible | `https://cn.tierflow.ai` | `claude` |
| Codex | OpenAI API | `https://cn.tierflow.ai/v1` | `codex` |

::: tip
TierFlow is compatible with both Anthropic API and OpenAI API. The Claude and Codex desktop setup in this guide routes requests through CC Switch local routing, so enable local routing and model mapping as shown below.
:::

## 1. Prerequisites

Make sure Node.js 18 LTS or later is installed:

```bash
node --version
npm --version
```

Make sure the CLI tools you want to manage are installed.

Claude Code:

```bash
claude --version
```

If it is not installed:

```bash
npm install -g @anthropic-ai/claude-code
# or macOS
brew install claude-code
```

Codex:

```bash
codex --version
```

If it is not installed:

```bash
npm install -g @openai/codex
# or macOS
brew install codex
```

## 2. Install CC Switch

Only download CC Switch from official channels:

- [CC Switch website](https://ccswitch.io/)
- [GitHub Releases](https://github.com/farion1231/cc-switch/releases)
- [GitHub repository](https://github.com/farion1231/cc-switch)

### Windows

1. Open [GitHub Releases](https://github.com/farion1231/cc-switch/releases).
2. Download `CC-Switch-v{version}-Windows.msi`.
3. Run the installer and follow the prompts.

You can also download `CC-Switch-v{version}-Windows-Portable.zip`, extract it, and run `CC-Switch.exe`.

### macOS

Homebrew is recommended:

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

Update:

```bash
brew upgrade --cask cc-switch
```

You can also download `CC-Switch-v{version}-macOS.dmg` from Releases and drag it into Applications.

### Linux

Debian / Ubuntu:

```bash
sudo dpkg -i CC-Switch-v{version}-Linux-*.deb
sudo apt-get install -f
```

Arch Linux:

```bash
paru -S cc-switch-bin
# or
yay -S cc-switch-bin
```

Generic AppImage:

```bash
chmod +x CC-Switch-v{version}-Linux-*.AppImage
./CC-Switch-v{version}-Linux-*.AppImage
```

After installation, launch CC Switch. On first launch, if existing Claude Code or Codex settings are found, CC Switch may import them as default providers.

<!-- Screenshot placeholder: CC Switch first launch and app switcher. -->

## 3. Configure Claude Code

::: warning
If you use the Claude Code desktop app, install a recent CC Switch version. Older versions may not include local routing support for Claude Desktop / Claude Code desktop, or may not show the routing and model mapping options below.
:::

1. Open CC Switch.
2. Confirm the top local routing switch is enabled, and that the Claude provider card shows `Routing required`.

![CC Switch Claude local routing switch](../../guide/assets/ccswitch-claude-routing-enabled.png)

3. Select `Claude Code` or the corresponding Claude Desktop app from the top bar or app switcher.
4. Click `+` in the upper-right corner to add a provider.
5. Select `Custom` to open the provider editor.
6. Fill in the basic information as follows:

| Item | Value |
|---|---|
| Provider name | `eucal` |
| Website | Optional |
| API Key | Your TierFlow API key |
| Request URL | `https://cn.tierflow.ai` |

![CC Switch Claude provider basics](../../guide/assets/ccswitch-claude-provider-basic.png)

Use your real TierFlow API key in the API Key field.

7. Enable `Model mapping required`.
8. Set API format to `Anthropic Messages (native)`.
9. Configure the common roles under `Model mapping`:

| Model role | Display name | Actual request model | Declare 1M support |
|---|---|---|---|
| Sonnet | `codex` | `claude` | Enabled |
| Opus | `claude` | `claude` | Enabled |
| Fable | `codex` | `claude` | Optional |
| Haiku | `claude` | `claude` | Enabled |

![CC Switch Claude model mapping](../../guide/assets/ccswitch-claude-model-mapping.png)

Save the provider, return to the Claude provider list, and enable `eucal`. CC Switch will route Claude requests through local routing and then forward them to TierFlow.

## 4. Configure Codex

1. Open CC Switch.
2. Go to `Settings` > `Routing`, confirm local routing is running, and enable `Codex` under routing-enabled apps.

![CC Switch Codex routing settings](../../guide/assets/ccswitch-codex-routing-settings.png)

3. Return to the app switcher and select `Codex`.
4. Click `+` in the upper-right corner to add a provider.
5. Select `Custom` to open the provider editor.
6. Fill in the basic information as follows:

| Item | Value |
|---|---|
| Provider name | `tierflow` |
| Website | Optional |
| API Key | Your TierFlow API key |
| API request URL | `https://cn.tierflow.ai/v1` |

![CC Switch Codex provider basics](../../guide/assets/ccswitch-codex-provider-basic.png)

7. Enable `Local routing required`.
8. Add this model under `Model mapping`:

| Display name | Actual request model | Context window |
|---|---|---|
| `codex` | `codex` | `1000000` |

![CC Switch Codex local routing and model mapping](../../guide/assets/ccswitch-codex-model-mapping.png)

9. Use the two config snippets below.

`auth.json`:

```json
{
  "OPENAI_API_KEY": "YOUR_API_KEY_HERE"
}
```

`config.toml`:

```toml
model_provider = "tierflow"
model = "codex"
disable_response_storage = true
preferred_auth_method = "apikey"

[model_providers.tierflow]
name = "tierflow"
base_url = "https://cn.tierflow.ai/v1"
wire_api = "responses"
```

Replace `YOUR_API_KEY_HERE` with your TierFlow API key.

Save the provider, return to the Codex provider list, and enable `tierflow`. CC Switch will write the Codex config files.

| System | auth.json | config.toml |
|---|---|---|
| Windows | `C:\Users\YOUR_USERNAME\.codex\auth.json` | `C:\Users\YOUR_USERNAME\.codex\config.toml` |
| macOS | `/Users/YOUR_USERNAME/.codex/auth.json` | `/Users/YOUR_USERNAME/.codex/config.toml` |
| Linux | `/home/YOUR_USERNAME/.codex/auth.json` | `/home/YOUR_USERNAME/.codex/config.toml` |

Keep local routing enabled while using this provider. After changing model mappings, restart Codex so the `/model` command can refresh the model list.

## 5. Verify

### Claude Code

Close the current terminal, reopen it, and enter any project directory:

```bash
cd your-project-folder
claude
```

In Claude Code, type:

```text
/status
```

Confirm the model is `claude`, then test:

```text
Reply exactly OK.
```

If Claude Code returns a normal response, the setup is complete.

### Codex

Close the current terminal, reopen it, and enter any project directory:

```bash
cd your-project-folder
codex
```

Send a simple test message:

```text
Reply exactly OK.
```

If Codex returns a normal response, the setup is complete.

## 6. Troubleshooting

### The new provider does not take effect

Restart the terminal, VS Code, Cursor, or Windows Terminal. Codex and Claude Code may load settings at startup, so already-running sessions may not pick up the latest config.

### Claude Code still uses official Claude

Check that the top CC Switch local routing switch is enabled, and confirm the active Claude provider is `eucal`. If you use the Claude Code desktop app, also confirm CC Switch is a recent version and that the Claude app card shows `Routing required`.

If old `ANTHROPIC_BASE_URL` or `ANTHROPIC_AUTH_TOKEN` values were set as system environment variables, remove them and reopen the terminal or Claude Code desktop app.

### Codex still uses official OpenAI

Check that the active CC Switch provider is `tierflow`, and confirm `config.toml` contains:

```toml
model_provider = "tierflow"
base_url = "https://cn.tierflow.ai/v1"
```

Also confirm `OPENAI_API_KEY` in `auth.json` has been replaced with your real TierFlow API key.

### Authentication failed

Check that the API key was copied completely and contains no extra spaces. For Claude and Codex, enter the API key in the CC Switch provider editor. If you also maintain config files manually, do not mix Claude's `ANTHROPIC_AUTH_TOKEN` with Codex's `OPENAI_API_KEY`.

### When is local routing needed?

For desktop setup, enable local routing for both Claude and Codex. Claude uses local routing to intercept desktop requests and apply model role mapping. Codex uses local routing to generate the model list and forward requests to `https://cn.tierflow.ai/v1`.
