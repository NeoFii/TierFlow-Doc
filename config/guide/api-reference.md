# API 参考

::: warning 文档完善中
此页面内容正在编写中，敬请期待。
:::

## 基础信息

| 项目 | 值 |
|------|---|
| Base URL | `https://cn.tierflow.ai/v1` |
| 认证方式 | Bearer Token |
| 兼容协议 | OpenAI API |

## Chat Completions

### 请求

```bash
POST /v1/chat/completions
```

### 请求体

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

### 参数说明

| 参数 | 类型 | 必填 | 说明 |
|-----|------|-----|------|
| `model` | string | 是 | 模型标识，支持 `auto`、`auto:cost`、`auto:quality` 或具体模型名 |
| `messages` | array | 是 | 对话消息数组 |
| `temperature` | number | 否 | 采样温度，0-2，默认 1 |
| `max_tokens` | integer | 否 | 最大生成 token 数 |
| `stream` | boolean | 否 | 是否流式输出，默认 false |

### 响应

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

## 错误码

| 状态码 | 说明 |
|-------|------|
| 400 | 请求参数错误 |
| 401 | 认证失败，检查 API Key |
| 429 | 请求过于频繁或超出预算 |
| 500 | 服务器内部错误 |
| 503 | 上游模型服务不可用 |
