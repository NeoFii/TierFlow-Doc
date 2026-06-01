# Quick Start

## Try It Online

Want to try TierFlow without installing anything? Send a request with cURL:

```bash
curl https://api.tierflow.ai/v1/chat/completions \
  -H "Authorization: Bearer your-tierflow-key" \
  -H "Content-Type: application/json" \
  -d '{"model": "auto", "messages": [{"role": "user", "content": "Hello"}]}'
```

## Integrate TierFlow

### Prerequisites

- Familiarity with the command line
- Python 3.8+ or Node.js 18+
- A TierFlow API Key

### Get Your API Key

Go to the [TierFlow Console](https://tierflow.dev/console) and create a new key on the "API Keys" page:

```
TIERFLOW_API_KEY=tf-sk-xxxxxxxxxxxxxxxxxxxxxxxx
```

### Install SDK

::: code-group

```bash [Python]
pip install openai
```

```bash [Node.js]
npm install openai
```

:::

TierFlow is compatible with the OpenAI SDK — no extra dependencies needed.

### Replace Base URL

Just change `base_url` and `api_key`. No other code changes required.

::: code-group

```python [Python]
from openai import OpenAI

client = OpenAI(
    api_key="tf-sk-xxxxxxxxxxxxxxxxxxxxxxxx",
    base_url="https://api.tierflow.ai/v1"
)

response = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "Explain vector databases in one sentence"}]
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
    messages: [{ role: "user", content: "Explain vector databases in one sentence" }]
});

console.log(response.choices[0].message.content);
```

```bash [cURL]
curl https://api.tierflow.ai/v1/chat/completions \
  -H "Authorization: Bearer tf-sk-xxxxxxxxxxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "auto",
    "messages": [{"role": "user", "content": "Explain vector databases in one sentence"}]
  }'
```

:::

That's it. Your requests are now intelligently routed through TierFlow.

## Routing Modes

The `model` field supports multiple routing strategies. Start with `auto`:

| Mode | model value | Description |
|------|-------------|-------------|
| Auto Route | `auto` | Automatically selects the optimal model based on task complexity (recommended) |

For more routing strategies (cost-first, quality-first, specific model, etc.), see [Routing Strategy](/en/guide/routing-strategy).

```python
response = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "Hello"}]
)
```

## View Routing Results

Each response includes routing metadata showing which model was actually used:

```json
{
  "model": "gpt-4o-mini",
  "tierflow": {
    "requested_model": "auto",
    "routed_model": "gpt-4o-mini",
    "route_reason": "simple_query",
    "estimated_cost": "$0.000042",
    "saved_vs_flagship": "82%"
  }
}
```

## Streaming

Works exactly like the OpenAI API — just use `stream=True`:

```python
stream = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "Write a short essay about AI"}],
    stream=True
)

for chunk in stream:
    print(chunk.choices[0].delta.content or "", end="")
```

## FAQ

### Does it affect response quality?

No. The routing engine evaluates each request's complexity and only downgrades when a lighter model can handle it. You can set quality thresholds in the console.

### Which models are supported?

OpenAI, Anthropic, Google, DeepSeek, Alibaba Cloud, and more. See [Model List](/en/guide/models) for the full list.

### How do I set budget limits?

Set daily/monthly limits in the console under "Budget Management". The API returns `429` when limits are exceeded.

## Next Steps

If you haven't read the [Introduction](/en/guide/introduction), we recommend starting there.

- [Routing Strategy](/en/guide/routing-strategy) — Deep dive into how the routing engine works.
- [Model List](/en/guide/models) — All supported models and pricing.
- [API Reference](/en/guide/api-reference) — Complete API documentation.
