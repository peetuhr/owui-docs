---
sidebar_position: 4
title: "Setting Up Image Generation"
---

# Setting Up Image Generation

Open WebUI can generate images—not just talk about them. Connect an image generation backend, and your AI can create visuals from text descriptions, edit existing images, or help you iterate on creative ideas.

This guide helps you choose the right approach and points you to the detailed setup instructions.

---

## How It Works

Image generation in Open WebUI follows a simple flow:

1. You provide a prompt (or ask the AI to write one for you)
2. The prompt goes to your configured image generation backend
3. The backend creates the image
4. The image appears in your chat

You can generate images directly by toggling image generation mode, or ask a text model to craft the perfect prompt first, then generate from that.

---

## Choosing a Backend

Your choice depends on your hardware, privacy requirements, and how much setup you're willing to do.

### Local Generation (Recommended)

For users who want images generated on their own hardware:

| Backend | Best For | Guide |
|---------|----------|-------|
| **ComfyUI** ⭐ | Most users—flexible, efficient, actively developed | [ComfyUI Setup →](../../../tutorials/images/comfyui) |
| **AUTOMATIC1111** | Users already familiar with A1111 | [AUTOMATIC1111 Setup →](../../../tutorials/images/automatic1111) |
| **SwarmUI** | Multi-user setups, batch generation | [SwarmUI Setup →](../../../tutorials/images/swarmui) |

**We recommend ComfyUI** for most local setups. It has a learning curve, but the investment pays off—better memory management, support for the latest models (SDXL, Flux), and a massive community building workflows and extensions.

### Cloud / API Options

No local GPU? These work immediately with just an API key:

| Backend | Best For | Guide |
|---------|----------|-------|
| **OpenAI DALL-E** | Quick setup, high quality | [OpenAI Setup →](../../../tutorials/images/openai) |
| **Image Router** | Access to multiple models through one API | [Image Router Setup →](../../../tutorials/images/image-router) [3] |

### Community Integrations

The community has built pipes and functions for additional services—Stability AI, Replicate, and others. Browse **Workspace → Functions** or the [community site](https://openwebui.com) for available integrations.

---

## Quick Comparison

| Approach | Pros | Cons |
|----------|------|------|
| **ComfyUI (Local)** | Private, no per-image cost, full control, latest models | Requires GPU, more setup |
| **AUTOMATIC1111 (Local)** | Simpler UI, large ecosystem | Higher memory usage than ComfyUI |
| **OpenAI DALL-E (Cloud)** | Zero setup, consistent quality | Per-image cost, requires internet, less control |
| **Image Router (Cloud)** | Access multiple models, one API | Per-image cost, requires internet |

---

## Using Image Generation

Once your backend is configured, you have two ways to generate:

**Direct generation** — Toggle **Image Generation** on in any chat, type your prompt, send. The image appears in the conversation.

**AI-assisted prompts** — Describe what you want to a text model, let it write an optimized prompt, then click the picture icon on its response to generate. Great for complex scenes or when you're not sure how to phrase things.

---

## Setup Guides

Ready to configure your chosen backend? Head to the detailed guide:

<div className="card-grid">

  <a className="card" href="../../../tutorials/images/comfyui">
    <h3>ComfyUI Setup</h3>
    <p>Our recommended local option. Powerful and flexible.</p>
  </a>

  <a className="card" href="../../../tutorials/images/automatic1111">
    <h3>AUTOMATIC1111 Setup</h3>
    <p>Popular Stable Diffusion interface.</p>
  </a>

  <a className="card" href="../../../tutorials/images/openai">
    <h3>OpenAI DALL-E Setup</h3>
    <p>Cloud-based, zero local requirements.</p>
  </a>

  <a className="card" href="../../../tutorials/images/">
    <h3>📂 View All Image Tutorials</h3>
    <p>Browse the full category of guides.</p>
  </a>

</div>

---

## What's Next?

Once image generation is working:

- **Experiment with different models** — Checkpoints dramatically affect style and quality
- **Combine with chat** — Use vision models to discuss and iterate on generated images
- **Explore workflows** — ComfyUI unlocks inpainting, upscaling, ControlNet, and more

Your AI can create now. What you make with it is up to you.