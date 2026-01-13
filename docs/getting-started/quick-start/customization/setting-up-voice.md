---
sidebar_position: 3
title: "Setting Up Voice"
---

# Setting Up Voice

Open WebUI supports full voice interaction—speak to your AI, have it speak back. This guide covers setting up both sides of that conversation: Speech-to-Text (STT) for understanding you, and Text-to-Speech (TTS) for responding out loud.

Once configured, you can have natural voice conversations, use voice input on mobile, or just listen to responses while doing other things.

---

## How Voice Works in Open WebUI

Voice interaction has two independent components:

| Component | What It Does | Direction |
|-----------|--------------|-----------|
| **Speech-to-Text (STT)** | Converts your voice into text the model can process | You → AI |
| **Text-to-Speech (TTS)** | Converts the AI's response into spoken audio | AI → You |

You can enable one without the other. Want to type but hear responses? Just set up TTS. Prefer to speak but read? Just configure STT. Want the full voice assistant experience? Set up both.

---

## Speech-to-Text (STT)

STT lets you talk to Open WebUI instead of typing. Click the microphone, speak, and your words become text.

### Built-in Options

Open WebUI includes STT support out of the box with multiple backends:

| Option | What It Is | Best For |
|--------|-----------|----------|
| **Browser Web API** | Uses your browser's built-in speech recognition | Quick setup, no configuration needed |
| **Local Whisper** | OpenAI's Whisper model running locally | Privacy-focused, works offline |
| **OpenAI Whisper API** | Cloud-based Whisper via OpenAI | High accuracy, requires API key |
| **Deepgram** | Third-party speech recognition service | High accuracy, real-time streaming |

### Configuration

Navigate to **Admin Settings → Audio** to configure your STT provider:

1. Select your preferred **Speech-to-Text Engine**
2. Configure any required API keys or endpoints
3. Test with the microphone button in any chat

For most users, the browser Web API works immediately with no setup. If you need higher accuracy or offline capability, local Whisper is the next step.

:::tip HTTPS Required
Browser microphone access requires HTTPS. If you're accessing Open WebUI over plain HTTP, speech input won't work. See the [Tailscale guide](../remote-access/tailscale-setup) for the easiest way to get HTTPS set up, or check out our [HTTPS tutorials](../advanced-topics/https-encryption) for other options.
:::

---

## Text-to-Speech (TTS)

TTS gives your AI a voice. Responses play as audio instead of (or in addition to) appearing as text.

### Built-in Options

| Option | What It Is | Best For |
|--------|-----------|----------|
| **Browser Web API** | Your browser's built-in speech synthesis | Instant setup, works everywhere |
| **OpenAI TTS** | OpenAI's voice API (alloy, echo, nova, etc.) | Natural-sounding voices, requires API key |
| **ElevenLabs** | Premium voice synthesis service | Most natural voices, supports EU endpoints |

### Configuration

Navigate to **Admin Settings → Audio** to configure TTS:

1. Select your preferred **Text-to-Speech Engine**
2. Choose a **voice** from the available options
3. Optionally enable **Auto-playback** to hear responses automatically

### Choosing a Voice

Each TTS engine offers different voices with distinct characteristics:

**Browser Web API** — Voices vary by operating system and browser. Quality ranges from robotic to surprisingly good depending on your setup.

**OpenAI TTS** — Six voices optimized for different tones:
- `alloy` — Neutral, balanced
- `echo` — Warmer, deeper
- `fable` — Expressive, British accent
- `onyx` — Deep, authoritative
- `nova` — Friendly, conversational
- `shimmer` — Soft, calm

**ElevenLabs** — Large voice library including the ability to clone voices. Higher quality but requires a paid subscription for significant use.

---

## Community TTS Options

The community has built integrations for additional TTS engines, giving you more choices—especially for self-hosted, privacy-focused, or specialized use cases:

| Engine | What It Offers |
|--------|---------------|
| **Edge TTS** | Microsoft's edge voices via Docker |
| **Kokoro** | Fast, lightweight TTS options |
| **Openedai-speech** | OpenAI-compatible TTS API you can self-host |
| **Chatterbox TTS** | Voice cloning capabilities |

These are community contributions—setup varies by project. Check the individual guides in the TTS documentation section for configuration details.

---

## Putting It Together: Conversation Mode

Once both STT and TTS are configured, you can use **Conversation Mode** for continuous back-and-forth dialogue.

### Starting a Voice Conversation

1. Open any chat
2. Click the **headphones icon** (or "Call" button) in the input area
3. Start speaking

The flow works like this:
1. You speak → STT converts to text
2. Text goes to the model → Response generated
3. Response text → TTS converts to audio
4. Audio plays → System waits for your next input

It's the closest thing to a natural conversation with AI.

### Tips for Better Voice Conversations

**Pause clearly when done speaking.** The system needs to detect silence to know you've finished.

**Create a voice-optimized model preset.** Default model responses often include markdown and long paragraphs—awkward when spoken aloud. See [Creating Your First Model Preset](./first-model-preset) for how to build an assistant that responds conversationally.

**Experiment with voices.** The right voice makes a significant difference in how natural conversations feel. Try a few before settling.

**Consider auto-playback settings.** Some people prefer responses to play automatically; others want to click play manually. Find what works for your use case.

---

## Troubleshooting

### Microphone not working

- Verify you're accessing Open WebUI over HTTPS
- Check browser permissions (look for microphone icon in address bar)
- Try a different browser to isolate the issue
- Ensure your microphone works in other applications

### TTS sounds robotic

- Try a different TTS engine (OpenAI and ElevenLabs sound more natural than browser defaults)
- Experiment with different voices within your chosen engine
- Check that your model preset isn't outputting markdown (sounds terrible when spoken)

### Long delay before audio plays

- Cloud TTS services (OpenAI, ElevenLabs) require network round-trips
- For lower latency, consider local/self-hosted TTS options
- Shorter responses play faster—consider a more concise system prompt

### Audio cuts off or skips

- Check your network connection for cloud TTS
- Some browsers handle audio streaming differently—try another browser
- Reduce response length if generating very long outputs

---

## What's Next?

Voice is configured. Now make it useful:

- **[Create a Voice Assistant preset](./first-model-preset)** — Optimize responses for spoken conversation
- **[Add Web Search](./adding-web-search)** — Let your voice assistant answer questions about current events
- **Explore community TTS options** — Find the voice that works best for you

Your AI can listen and speak. What you talk about is up to you.