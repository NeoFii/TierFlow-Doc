# 快速开始

## 线上体验

想在不安装任何东西的情况下快速体验 TierFlow？直接使用 cURL 发送一个请求：

```bash
curl https://api.tierflow.ai/v1/chat/completions \
  -H "Authorization: Bearer your-tierflow-key" \
  -H "Content-Type: application/json" \
  -d '{"model": "auto", "messages": [{"role": "user", "content": "你好"}]}'
```

## 接入 TierFlow

### 前提条件

- 熟悉命令行操作
- Python 3.8+ 或 Node.js 18+
- 一个 TierFlow API Key

### 获取 API Key

前往 [TierFlow 控制台](https://tierflow.dev/console)，在「API 密钥」页面创建新的密钥：

```
TIERFLOW_API_KEY=tf-sk-xxxxxxxxxxxxxxxxxxxxxxxx
```

### 安装 SDK

::: code-group

```bash [Python]
pip install openai
```

```bash [Node.js]
npm install openai
```

:::

TierFlow 兼容 OpenAI SDK，无需安装额外依赖。

### 替换 Base URL

只需修改 `base_url` 和 `api_key`，其他代码无需任何改动。

::: code-group

```python [Python]
from openai import OpenAI

client = OpenAI(
    api_key="tf-sk-xxxxxxxxxxxxxxxxxxxxxxxx",
    base_url="https://api.tierflow.ai/v1"
)

response = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "用一句话解释什么是向量数据库"}]
)

print(response.choices[0].message.content)
```

```javascript [Node.js]
import OpenAI from "openai";

const client = new OpenAI({
    apiKey: "tf-sk-xxxxxxxxxxxxxxxxxxxxxxxx",
    baseURL: "https://api.tierflow.ai/v1"
});

const response = await client.chat.completions.create({
    model: "auto",
    messages: [{ role: "user", content: "用一句话解释什么是向量数据库" }]
});

console.log(response.choices[0].message.content);
```

```bash [cURL]
curl https://api.tierflow.ai/v1/chat/completions \
  -H "Authorization: Bearer tf-sk-xxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "auto",
    "messages": [{"role": "user", "content": "用一句话解释什么是向量数据库"}]
  }'
```

:::

就这么简单。你的请求已经通过 TierFlow 智能路由了。

## 路由模式

`model` 字段支持多种路由策略，这里先使用 `auto`（自动路由）即可：

| 模式 | model 值 | 说明 |
|------|----------|------|
| 自动路由 | `auto` | 根据任务复杂度自动选择最优模型（推荐） |

更多路由策略（成本优先、质量优先、指定模型等）请参阅 [路由策略详解](/guide/routing-strategy)。

```python
response = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "你好"}]
)
```

## 流式输出

与 OpenAI API 用法完全一致，使用 `stream=True` 即可：

```python
stream = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "写一篇关于AI的短文"}],
    stream=True
)

for chunk in stream:
    print(chunk.choices[0].delta.content or "", end="")
```

## 常见问题

### 会影响响应质量吗？

不会。路由引擎会评估每个请求的复杂度，只在模型能力足以胜任时才进行降级路由。你可以在控制台设置质量下限阈值。

### 支持哪些模型？

已接入 OpenAI、Anthropic、Google、DeepSeek、阿里云等主流供应商。完整列表见 [模型列表](/guide/models)。

### 如何设置预算上限？

在控制台「预算管理」中设置每日/每月上限，超过限额后 API 返回 `429` 状态码。

## 下一步

如果你还没有阅读 [简介](/guide/introduction)，建议先了解 TierFlow 的设计理念。

- [路由策略详解](/guide/routing-strategy) — 深入了解路由引擎的工作原理。
- [模型列表](/guide/models) — 查看所有支持的模型和定价。
- [API 参考](/guide/api-reference) — 完整的接口文档和参数说明。
