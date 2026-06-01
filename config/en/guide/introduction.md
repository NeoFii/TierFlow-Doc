# Introduction

## What is TierFlow?

TierFlow is an LLM token optimization and intelligent dispatch platform for agentic AI applications. It exposes a unified OpenAI-compatible API, connects multiple models and providers, and uses the in-house BrainNet-8B task perception engine to analyze intent, context, complexity, model capability, cost, and availability at each step.

For developers, integration stays simple: keep your existing OpenAI SDK call pattern, replace `base_url`, and set the model to `auto`. TierFlow handles model selection, context refinement, retries, and cost control after that.

Here's a minimal integration example:

```python
from openai import OpenAI

client = OpenAI(
    api_key="your-tierflow-key",
    base_url="https://api.tierflow.ai/v1"
)

response = client.chat.completions.create(
    model="auto",
    messages=[{"role": "user", "content": "Hello"}]
)
```

The code above demonstrates two core features:

- **Unified Interface**: Compatible with the OpenAI SDK. Existing code only needs a `base_url` change.
- **Intelligent Routing**: `model="auto"` lets TierFlow match the model based on task stage, context, and cost constraints.

> Already familiar with these concepts? Jump straight to [Quick Start](/en/guide/getting-started).

## The Problem

Production AI applications and agent workflows often run into the same bottlenecks:

- **Uncontrolled Token Cost**: Long task chains consume large contexts, and sending every step to flagship models quickly raises cost.
- **Model Selection Overhead**: Reasoning, coding, retrieval, summarization, and tool use often require different model strengths.
- **Context Redundancy**: Multi-step workflows accumulate repeated or low-value context, increasing latency and spend.
- **Provider Availability Risk**: Rate limits, outages, or price changes from a single provider can disrupt production workloads.

TierFlow is designed to make every model call more suitable, more stable, and less expensive without sacrificing output quality.

## Intelligent Routing Platform

At the center of TierFlow is BrainNet-8B, a task perception model for step-level routing. Instead of relying on static rules, it evaluates what the current step needs, which context should be retained, which model is the best fit, and how to balance quality, latency, and cost.

You can use TierFlow as:

- An OpenAI-compatible gateway for automatic routing with minimal code changes.
- A multi-model gateway that unifies providers, models, keys, and quotas.
- An agent dispatch layer that maps each step to the right model and execution path.
- A high-availability inference entry point that switches paths during failures, rate limits, or cost changes.

The core flow is always the same: **perceive task -> refine context -> match model -> route execution**.

## Routing Decisions

BrainNet-8B converts each request into routing signals and combines them into a step-level decision:

- **Task Understanding**: Identifies user intent, constraints, tool requirements, and key inputs.
- **Complexity Assessment**: Decides whether a high-capability model is needed or a lightweight model is enough.
- **Context Compression**: Keeps the essential context and reduces unnecessary token usage.
- **Model Capability Mapping**: Matches model strengths across coding, reasoning, summarization, and tool use.
- **Cost Prediction**: Considers budget, latency, success rate, and model pricing in one decision.
- **Decision Output**: Selects the model, provider, and execution path.

## Use Cases

TierFlow is a fit for applications that continuously call LLM APIs:

- **AI Agents**: Route different steps in a task chain to different model tiers.
- **SaaS Products**: Reduce average cost across high-volume workloads with many simple requests.
- **Developer Tools**: Dynamically assign models for code explanation, fixes, test generation, and documentation.
- **Enterprise Tools**: Control API budgets while preserving higher-quality reasoning for critical tasks.

## Still Have Questions?

Check the [Quick Start](/en/guide/getting-started) for common questions.

## Pick Your Learning Path

- [Quick Start](/en/guide/getting-started): Get integrated in 5 minutes.
- [Routing Strategy](/en/guide/routing-strategy): Learn how the routing engine works.
- [API Reference](/en/guide/api-reference): Review the complete API documentation and parameters.
