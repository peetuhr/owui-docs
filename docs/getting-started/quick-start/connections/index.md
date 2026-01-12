---
sidebar_position: 1
title: "Connections"
---

# Connect Your Models

Open WebUI is the interface. Now it needs something to talk to.

The good news: you're not locked into one provider. Connect local models through Ollama, cloud models through OpenAI, or mix both. Add more anytime. Switch between them mid-conversation if you want.

This flexibility is the point. Your setup, your rules.

---

## Choose Your Starting Point

<div className="card-grid">

  <a className="card" href="/starting-with-ollama">
    <h3>🦙 Ollama</h3>
    <p><strong>Best for:</strong> Running models locally on your own hardware</p>
    <p>The fastest path to local AI. Download models with a single command, run them on your CPU or GPU. No cloud, no API keys, no ongoing costs.</p>
  </a>

  <a className="card" href="/starting-with-openai">
    <h3>🔑 OpenAI</h3>
    <p><strong>Best for:</strong> Direct access to GPT-4, o1, and OpenAI's latest models</p>
    <p>Connect with your API key. Simple setup, powerful models, pay-per-use pricing.</p>
  </a>

  <a className="card" href="/starting-with-openai-compatible">
    <h3>🔌 OpenAI-Compatible APIs</h3>
    <p><strong>Best for:</strong> Other providers, self-hosted servers, or mixing multiple sources</p>
    <p>Works with Gemini, Claude (via proxy), vLLM, Llama.cpp, LiteLLM, Together AI, Mistral, Groq—anything that speaks the OpenAI format.</p>
  </a>

  <a className="card" href="/starting-with-functions">
    <h3>⚡ Functions</h3>
    <p><strong>Best for:</strong> Providers without OpenAI-compatible endpoints, or custom integrations</p>
    <p>Direct API access to Claude, Bedrock, Vertex AI, and more. Also the foundation for building custom tools and pipelines.</p>
  </a>

</div>

---

## Not Sure Which to Choose?

**Start with one.** You can always add more later.

| If you want... | Start here |
|----------------|------------|
| Everything running locally, no cloud | **Ollama** |
| The most capable models, simplest setup | **OpenAI** |
| A specific provider (Gemini, Mistral, Groq, etc.) | **OpenAI-Compatible** |
| Claude, Bedrock, or something custom | **Functions** |
| All of the above | Start with any one, add the rest later |

:::info Mix and Match
Open WebUI handles multiple providers simultaneously. Many users run Ollama for local models *and* connect OpenAI for tasks that need more capability. You're not choosing forever—you're choosing where to start.
:::

---

## After You Connect

Once you've got at least one provider working:

→ **[Customize your setup](../customization)** — Add web search, voice, image generation, and model presets

→ **[Set up remote access](../remote-access)** — Use Open WebUI from any device, anywhere

<!-- 
Screenshot opportunity: The model selector dropdown showing multiple connected providers (e.g., Ollama models + OpenAI models in the same list). This reinforces the "mix and match" message.
-->