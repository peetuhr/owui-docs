---
sidebar_position: 1
title: "Adding Web Search"
---

# Adding Web Search

Your AI knows a lot—but it doesn't know what happened yesterday. Web search bridges that gap.

When you enable web search, your assistant can pull in current information before responding. News, documentation, recent events—anything the model's training data doesn't cover. It's the difference between "I don't have information past my training cutoff" and an actual answer.

---

## How It Works

When web search is enabled for a conversation:

1. Your query goes to the search provider you've configured
2. Open WebUI retrieves relevant results
3. Those results get passed to the model as context
4. The model responds using both its training *and* the fresh information

You control when this happens. Web search is a per-conversation toggle—not always-on by default.

---

## Choosing a Search Provider

Open WebUI supports a wide range of search backends. Which one you choose depends on what matters to you:

### Self-Hosted (Maximum Privacy)

| Provider | What It Is | Best For |
|----------|-----------|----------|
| [**SearXNG**](../../../features/web-search/searxng) ⭐ | Privacy-respecting metasearch engine you run yourself | Our recommended option. No API keys, no external accounts, fully under your control. |
| [**Yacy**](../../../features/web-search/yacy) | Peer-to-peer search engine | Decentralized search without relying on any external service |

### Free Tier Available

| Provider | What It Is | Best For |
|----------|-----------|----------|
| [**DDGS**](../../../features/web-search/ddgs) | DuckDuckGo search | Quick setup, no API key required |
| [**Jina**](../../../features/web-search/jina) | AI-focused search API | Good free tier, optimized for LLM consumption |
| [**Brave**](../../../features/web-search/brave) | Brave Search API | Privacy-focused, generous free tier |
| [**Tavily**](../../../features/web-search/tavily) | Search API built for AI agents | Designed specifically for LLM use cases |

### Paid / API Key Required

| Provider | What It Is | Best For |
|----------|-----------|----------|
| [**Google PSE**](../../../features/web-search/google-pse) | Google Programmable Search Engine | Google-quality results, requires setup |
| [**Bing**](../../../features/web-search/bing) | Microsoft Bing Search API | Strong results, Azure integration |
| [**Kagi**](../../../features/web-search/kagi) | Premium search engine | High-quality results if you're already a Kagi subscriber |
| [**Serper**](../../../features/web-search/serper) | Google results via API | Google results without PSE setup |
| [**Serply**](../../../features/web-search/serply) | Google results via API | Alternative Google results provider |
| [**Serpstack**](../../../features/web-search/serpstack) | Google results via API | Another Google results option |
| [**SerpApi**](../../../features/web-search/serpapi) | Google results via API | Established Google scraping service |
| [**SearchApi**](../../../features/web-search/searchapi) | Multi-engine API | Multiple search engines in one |
| [**Exa AI**](../../../features/web-search/exa) | Neural search API | Semantic search, good for research queries |
| [**Mojeek**](../../../features/web-search/mojeek) | Independent search engine | No tracking, UK-based |
| [**Perplexity**](../../../features/web-search/perplexity) | AI-powered search | Perplexity's answer synthesis |

### Other Options

| Provider | What It Is | Best For |
|----------|-----------|----------|
| [**External**](../../../features/web-search/external) | Custom endpoint | Rolling your own search integration [1] |

---

## Our Recommendation: SearXNG

If you're running Open WebUI locally and care about privacy, **SearXNG** is the way to go.

Why?

- **No API keys.** No accounts. No usage limits.
- **Self-hosted.** Searches don't leave your network.
- **Metasearch.** Aggregates results from multiple engines (Google, Bing, DuckDuckGo, and more) without those engines knowing who's searching.
- **Already containerized.** Fits right into your Docker workflow.

The tradeoff: you're running another service. If you want something simpler, DDGS or Jina are solid starting points with minimal setup.

👉 [**Set up SearXNG**](../../../features/web-search/searxng)

---

## Enabling Web Search

Once you've configured a provider in **Admin Settings → Web Search**, using it is straightforward:

1. Open a chat
2. Click the **+** button next to the message input
3. Toggle **Web Search** on
4. Ask your question

The search results will be included in your model's context for that response.

:::tip
Web search toggles off when you start a new chat. It's intentionally per-conversation—you probably don't want every casual question hitting a search API.
:::

---

## What's Next?

Web search gives your assistant access to the live web. For information that's *yours*—documents, notes, internal knowledge—check out [**RAG (Retrieval-Augmented Generation)**](/features/rag) in the Features section.