# Codex 接入 TierFlow 教程

本文介绍如何把 OpenAI Codex CLI 接入 TierFlow。

基础信息：

| 项目 | 值 |
|---|---|
| Base URL | `https://api.tierflow.ai/v1` |
| 认证方式 | Bearer Token |
| 兼容协议 | OpenAI API |
| Model | `codex` |

## 1. 确认 Codex 已安装

```bash
codex --version
```

如果未安装，使用 npm 全局安装：

```bash
npm install -g @openai/codex
# 或者 / or
brew install codex
```

## 2. 创建.codex目录

若目录已存在请先删除，再重新创建（在文件资源管理器或 PowerShell 中操作）：

```bash
# PowerShell
Remove-Item -Recurse -Force ~\.codex -ErrorAction SilentlyContinue
New-Item -ItemType Directory ~\.codex
```
> 将 `<your-username>` 替换为你的实际 Windows 用户名。


## 3. 获取API密钥

前往控制台的 「获取API」 页面，创建一个新密钥并复制。



## 4. 创建 auth.json

在 `C:\Users\<your-username>\.codex` 路径下，删除已有的 auth.json（若有），新建一个：

```bash
{
  "OPENAI_API_KEY": "YOUR_API_KEY"
}
```
> 将 YOUR_API_KEY 替换为上一步复制的密钥。


## 5. 创建 config.toml

在 `C:\Users\<your-username>\.codex` 路径下，删除已有的 config.toml（若有），新建一个：

确认环境变量已生效：

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

以上内容请原封不动粘贴，不要修改任何值。

## 6. 重启终端 验证安装

重启终端后运行以下命令，确认安装成功：

```bash
codex -V
```
> 若输出版本号，则说明 Codex 已正确安装。


## 7. 开始使用 Codex

进入任意项目目录，启动 Codex：

```bash
# 切换到项目目录 / Navigate to project
cd your-project-folder

# 启动 Codex / Launch Codex
codex
```