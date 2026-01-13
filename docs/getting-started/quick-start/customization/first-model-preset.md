---
sidebar_position: 2
title: "Creating Your First Model Preset"
---

# Creating Your First Model Preset

Open WebUI's model system lets you create custom "presets"—configurations that wrap any base model with your own system prompts, knowledge, tools, and settings. Think of it as creating specialized assistants for different tasks, all powered by the models you already have.

---

## What Is a Model Preset?

A model preset is a saved configuration that includes:

- **A base model** — The actual AI doing the work (GPT-4, Llama 3, Claude, etc.)
- **A system prompt** — Instructions that shape how the model responds
- **Optional additions** — Knowledge bases, tools, specific parameters

When you select a preset, you're not downloading a new model—you're applying a custom configuration to an existing one. One base model can power dozens of different presets.

---

## Why Create Presets?

Without presets, you'd copy-paste the same instructions into every chat. With presets, you create once and use forever.

**Common examples:**

| Preset | What It Does |
|--------|--------------|
| **Voice Assistant** | Responds conversationally without markdown—optimized for text-to-speech |
| **Code Reviewer** | Analyzes code for bugs, security issues, and style problems |
| **Writing Editor** | Provides feedback on clarity, structure, and tone |
| **Meeting Summarizer** | Extracts action items, decisions, and key points from transcripts |
| **Research Assistant** | Synthesizes information with citations and balanced perspectives |
| **Language Tutor** | Teaches through conversation, corrects mistakes gently |

You get the idea. Same model, different personalities and capabilities.

---

## Creating Your First Preset: A Voice Assistant

Let's walk through creating a preset optimized for voice conversations—one that responds naturally when spoken aloud rather than formatting everything in markdown.

### Step 1: Open the Model Builder

1. Click **Workspace** in the sidebar
2. Select **Models**
3. Click **+ Create a Model**

### Step 2: Configure the Basics

| Field | What to Enter |
|-------|---------------|
| **Name** | `Voice Assistant` |
| **Model ID** | `voice-assistant` (auto-generated, customize if you want) |
| **Base Model** | Choose your preferred model—`llama3`, `gpt-4o`, `claude-3-sonnet`, whatever you have connected |
| **Description** | `Conversational assistant optimized for voice interaction` |

### Step 3: Add the System Prompt

The system prompt is where you define the assistant's behavior. For a voice assistant, we want responses that sound natural when spoken—no bullet points, no markdown, no walls of text.

In the **System Prompt** field, enter something like:

```text
You are a voice assistant. Respond conversationally, as if speaking out loud.

Guidelines:
- Keep responses concise—2-3 sentences for simple questions
- Never use markdown formatting (no bullets, headers, bold, or code blocks)
- Use natural language instead of lists ("There are three things: first... second... third...")
- Use contractions naturally (I'm, you're, don't)
- Match the user's tone—casual questions get casual answers

The user is listening, not reading. Optimize for the ear.
```

:::tip Finding Prompts
This is just a starting point. The [Open WebUI Community](https://openwebui.com) has hundreds of shared prompts, presets, and configurations you can use directly or adapt. No need to start from scratch every time.
:::

### Step 4: Save and Pin

1. Click **Save**
2. Back in the Models list, find your Voice Assistant
3. Click the **⋮** menu → **Pin to Sidebar**

Your preset now appears in the sidebar for one-click access.

---

## Other Preset Ideas

The voice assistant is just one example. Here are prompts for other useful presets:

### Code Reviewer

```text
You are a senior software engineer reviewing code. For each piece of code shared:

1. Identify bugs or potential runtime errors
2. Note security concerns if any
3. Suggest improvements for readability and maintainability
4. Be direct—don't pad feedback with excessive praise

If the code looks good, say so briefly and move on.
```

### Writing Editor

```text
You are an experienced editor. When given text to review:

- Focus on clarity and structure first, grammar second
- Explain *why* something doesn't work, not just that it doesn't
- Preserve the author's voice—don't rewrite everything in your style
- Be encouraging but honest

Ask clarifying questions if the intended audience or purpose isn't clear.
```

### Meeting Summarizer

```text
You summarize meeting transcripts. For each transcript:

1. Key decisions made (if any)
2. Action items with owners (if mentioned)
3. Open questions or unresolved topics
4. One-paragraph summary of the discussion

Be concise. No one wants a summary longer than the meeting.
```

### Research Assistant

```text
You help with research by synthesizing information clearly.

- Present multiple perspectives when topics are contested
- Distinguish between established consensus and emerging/minority views
- Note limitations in your knowledge (training cutoff, etc.)
- When asked for sources, be honest about what you can and can't verify

Aim for useful, not exhaustive.
```

---

## Advanced Options

Once you're comfortable with basic presets, explore these additional capabilities:

### Knowledge Bases

Attach documents, files, or collections to your preset. The model will reference them when responding—useful for company wikis, personal notes, or domain-specific information.

### Tools

Give your preset the ability to *do* things: search the web, run code, generate images, query APIs. Tools transform passive assistants into active agents.

### Parameters

Fine-tune temperature, context length, and other model settings per-preset. A creative writing assistant might want higher temperature; a code reviewer wants lower.

### Tags

Organize presets with tags. When you have a dozen presets, `#work`, `#personal`, `#voice`, `#coding` make them findable.

---

## Sharing Your Presets

Built something useful? You can share presets with specific users, groups, or the broader Open WebUI community.

From the Models list:
1. Click the **⋮** menu on any preset
2. Select sharing options

What you keep private stays private. What you share helps others. That's the balance we're going for.

---

## What's Next?

You've created a custom preset. From here:

- **Set up voice input/output** — Make that voice assistant actually speak
- **Add web search** — Let your assistants access current information
- **Explore the community** — Find prompts and presets others have shared

The model is the engine. The preset is what makes it *yours*.
```