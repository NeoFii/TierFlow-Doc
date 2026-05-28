# Introduction

## What is TierFlow?

TierFlow provides a unified API interface that automatically selects the optimal model based on request content, significantly reducing costs without compromising output quality.

Here's a minimal integration example:

```python
from openai import OpenAI

client = OpenAI(
    api_key="your-tierflow-key",
    base_url="https://api.tierflow.dev/v1"
)

response = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "Hello"}]
)
```

The code above demonstrates two core features:

- **Unified Interface**: Compatible with the OpenAI SDK — just replace `base_url` to get started.
- **Intelligent Routing**: `model="auto"` lets TierFlow automatically match the optimal model for each request.

> Already familiar with these concepts? Jump straight to [Quick Start](/en/guide/getting-started).

## The Problem

Developers using LLM APIs face several common pain points:

- **High Costs**: Flagship models are expensive, but most requests don't need that level of capability.
- **Choice Paralysis**: Too many models, each with different strengths — hard to pick the right one for each task.
- **Vendor Lock-in**: Each provider has a different API format, making migration costly.
- **Availability Risk**: A single provider outage means your service goes down.

TierFlow is designed to solve all of these at once.

## An Intelligent Routing Platform

"TierFlow is a routing engine and a model ecosystem."

Depending on your needs, you can use TierFlow as:

- A drop-in replacement for the OpenAI API — zero-effort cost reduction
- A multi-model gateway — unified key and quota management across all providers
- An intelligent dispatch layer — automatically assigns model tiers based on task complexity
- A high-availability solution — automatic failover to backup providers

Regardless of the use case, the core logic is the same: **analyze request → match model → route call**. That's why TierFlow is called an "intelligent routing platform" — it's a unified entry point that adapts to your needs.

## Routing Decisions

TierFlow's routing engine makes decisions based on multiple dimensions:

- **Task Complexity**: Analyzes request content to determine whether a flagship or lightweight model is sufficient.
- **Latency Awareness**: Real-time monitoring of API response times across all models, avoiding high-latency nodes.
- **Cost Optimization**: Prioritizes cost-effective models while meeting quality requirements.
- **Failover**: Automatically switches to equivalent backup models when a provider has issues — zero downtime.

## Use Cases

TierFlow works for any scenario that involves LLM API calls:

- **SaaS Products**: High request volume with diverse complexity — most queries don't need flagship models.
- **AI Agents**: Multi-step task chains where different steps have different complexity levels.
- **Content Generation**: Translations and summaries use lightweight models; creative writing uses flagship models.
- **Enterprise Tools**: Control API budgets while ensuring critical tasks get top-quality output.

## Still Have Questions?

Check the [Quick Start](/en/guide/getting-started) for common questions.

## Pick Your Learning Path

- [Quick Start](/en/guide/getting-started) — Get integrated in 5 minutes.
- [Routing Strategy](/en/guide/routing-strategy) — Deep dive into how the routing engine works.
- [API Reference](/en/guide/api-reference) — Complete interface documentation.
