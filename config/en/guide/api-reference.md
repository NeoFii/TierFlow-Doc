# API Reference

::: warning Work in Progress
This page is under construction. Stay tuned!
:::

## Basic Information

| Item | Value |
|------|-------|
| Base URL | `https://api.tierflow.ai/v1` |
| Authentication | Bearer Token |
| Protocol | OpenAI API Compatible |

## Chat Completions

### Request

```bash
POST /v1/chat/completions
```

### Request Body

```json
{
  "model": "auto",
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ],
  "temperature": 0.7,
  "max_tokens": 1000,
  "stream": false
}
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `model` | string | Yes | Model identifier. Supports `auto`, `auto:cost`, `auto:quality`, or specific model names |
| `messages` | array | Yes | Array of conversation messages |
| `temperature` | number | No | Sampling temperature, 0-2, default 1 |
| `max_tokens` | integer | No | Maximum tokens to generate |
| `stream` | boolean | No | Enable streaming output, default false |

### Response

```json
{
  "id": "chatcmpl-abc123",
  "object": "chat.completion",
  "created": 1699000000,
  "model": "gpt-4o-mini",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I help you today?"
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 20,
    "completion_tokens": 10,
    "total_tokens": 30
  },
  "mindrouter": {
    "requested_model": "auto",
    "routed_model": "gpt-4o-mini",
    "route_reason": "simple_query",
    "estimated_cost": "$0.000018",
    "latency_ms": 320
  }
}
```

## Error Codes

| Status Code | Description |
|-------------|-------------|
| 400 | Bad request parameters |
| 401 | Authentication failed, check API Key |
| 429 | Rate limited or budget exceeded |
| 500 | Internal server error |
| 503 | Upstream model service unavailable |
