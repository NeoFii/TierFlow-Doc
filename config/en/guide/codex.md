# Codex TierFlow Setup

This guide explains how to connect OpenAI Codex CLI to TierFlow.

Basic info:

| Item | Value |
|---|---|
| Base URL | `https://api.tierflow.ai/v1` |
| Auth | Bearer Token |
| Protocol | OpenAI API |
| Model | `codex` |

## 1. Confirm Codex is Installed

```bash
codex --version
```

If not installed, install globally via npm:

```bash
npm install -g @openai/codex
# or
brew install codex
```

## 2. Create .codex Directory

If the directory already exists, delete and recreate it (via File Explorer or PowerShell):

```bash
# PowerShell
Remove-Item -Recurse -Force ~\.codex -ErrorAction SilentlyContinue
New-Item -ItemType Directory ~\.codex
```
> Replace `<your-username>` with your actual Windows username.


## 3. Get API Key

Go to the console's "Get API" page, create a new key and copy it.



## 4. Create auth.json

At `C:\Users\<your-username>\.codex`, delete the existing auth.json (if any) and create a new one:

```bash
{
  "OPENAI_API_KEY": "YOUR_API_KEY"
}
```
> Replace YOUR_API_KEY with the key you copied in the previous step.


## 5. Create config.toml

At `C:\Users\<your-username>\.codex`, delete the existing config.toml (if any) and create a new one:

```bash
model_provider = "tierflow"
model = "codex"
disable_response_storage = true
preferred_auth_method = "apikey"

[model_providers.tierflow]
name = "tierflow"
base_url = "https://api.tierflow.ai/v1"
wire_api = "responses"
```

Paste the above content exactly as-is. Do not modify any values.

## 6. Restart Terminal & Verify

Restart your terminal and run the following command to confirm installation:

```bash
codex -V
```
> If a version number is displayed, Codex is correctly installed.


## 7. Start Using Codex

Navigate to any project directory and launch Codex:

```bash
# Navigate to project
cd your-project-folder

# Launch Codex
codex
```
