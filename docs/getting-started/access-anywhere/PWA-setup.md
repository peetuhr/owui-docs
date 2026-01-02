# Installing Open WebUI as a Progressive Web App (PWA)

## Why Install as a PWA?

You've got Tailscale running. You can access Open WebUI from anywhere. But opening a browser, typing a URL, waiting for it to load—it still *feels* like a website.

A Progressive Web App changes that. One tap from your home screen and you're in. Full screen. No browser chrome. It looks and feels like a native app, because for most purposes, it *is* one.

On mobile, this also unlocks features browsers don't always allow—like microphone access for voice input. More on that in a moment.

### TL;DR

- **What this does**: Adds Open WebUI to your home screen as an app-like shortcut with fullscreen mode
- **What you need**: A working Open WebUI instance served over HTTPS (like through Tailscale)
- **What you get**: Native app feel, one-tap access, voice input support on mobile

---

## Before You Start

PWAs require HTTPS. If you're accessing Open WebUI over plain HTTP (like `http://192.168.1.50:3000`), the "install" option won't appear, and features like microphone access will be blocked.

**If you followed the Tailscale guide**, you're already set—Tailscale Serve provides HTTPS automatically.

**If you didn't set up Tailscale** (or another HTTPS solution), here's what you're working with:

| Without HTTPS | With HTTPS |
|---------------|------------|
| Can't install as PWA | Full PWA support |
| No microphone access on mobile | Voice input works |
| Only accessible on your local network | Accessible from anywhere (with Tailscale) |
| Browser shows "not secure" warning | Clean, trusted connection |

If you need HTTPS but don't want Tailscale, check out the "Enabling HTTPS Encryption" guide in Advanced Topics. But honestly? Tailscale is probably easier.

---

## Installing on iOS

Safari is the only browser that can install PWAs on iOS. Chrome, Firefox, and others don't have this capability—Apple's rules.

### Steps

1. Open Safari and navigate to your Open WebUI URL (e.g., `https://open-webui.your-tailnet.ts.net`)
2. Tap the **Share** button (the square with an arrow pointing up)
3. Scroll down and tap **Add to Home Screen**
4. Name it whatever you want—"Open WebUI" or just "AI" if you're feeling minimal
5. Tap **Add**

That's it. You'll see the Open WebUI icon on your home screen. Tap it, and it launches in fullscreen—no Safari UI, no tabs, no URL bar. Just your AI.

### Voice Input on iOS

Once installed as a PWA over HTTPS, you can use the microphone for voice input. The first time you try, iOS will ask for permission. Grant it, and you're set.

If you're *not* using HTTPS, the microphone option either won't appear or won't work. This is a browser security restriction, not an Open WebUI limitation.

---

## Installing on Android

Android gives you more flexibility—Chrome, Edge, and most Chromium-based browsers support PWA installation.

### Steps (Chrome)

1. Open Chrome and navigate to your Open WebUI URL
2. Tap the **three-dot menu** in the top right
3. Tap **Add to Home screen** (or **Install app** if Chrome detects the PWA manifest)
4. Name it and tap **Add**

Some Android versions also show an "Install" prompt automatically in the address bar when you visit a PWA-capable site.

### Voice Input on Android

Same deal as iOS—HTTPS is required for microphone access. Once you've installed the PWA and granted microphone permissions, voice input works seamlessly.

---

## Installing on Desktop

PWAs aren't just for mobile. If you want a dedicated window for Open WebUI on your laptop or desktop, you can install it there too.

### Chrome / Edge

1. Navigate to your Open WebUI URL
2. Look for the install icon in the address bar (usually a monitor with a down arrow, or a + symbol)
3. Click it and confirm

Alternatively: **three-dot menu → Install Open WebUI** (or "Install app")

### Firefox

Firefox doesn't support PWA installation on desktop. You'll need to use Chrome, Edge, or another Chromium-based browser.

### What You Get

- A dedicated app window (no tabs, no URL bar)
- Open WebUI appears in your app launcher/dock
- Keyboard shortcuts like `Cmd+Tab` or `Alt+Tab` switch to it like any other app

---

## What PWAs Can't Do

Let's be honest about the limitations:

- **No push notifications** (yet)—Open WebUI doesn't currently send them anyway, but even if it did, PWA notification support is inconsistent
- **No offline access**—you need to reach your server; the PWA is just a wrapper, not a cached copy of the whole app
- **iOS restrictions**—Apple limits what PWAs can do compared to native apps; for example, you can't change the app icon dynamically

For most users, none of this matters. You're here for quick access and voice input, and you've got both.

---

## Troubleshooting

**Don't see the "Add to Home Screen" option?**
- Make sure you're using HTTPS
- On iOS, make sure you're using Safari (not Chrome or Firefox)
- Try refreshing the page

**Microphone not working?**
- Check that you've granted microphone permissions to the PWA
- Verify you're on HTTPS—`http://` won't work
- On iOS, make sure you installed from Safari, not another browser

**PWA looks weird or doesn't go fullscreen?**
- Try removing it from your home screen and reinstalling
- Clear your browser cache before reinstalling

**Installed on desktop but it opens in a browser tab instead?**
- You may have added a bookmark instead of installing the PWA
- Look for the specific "Install" option, not just "Add to bookmarks"

---

## What's Next?

You've got a private AI assistant you can access from anywhere, running as a proper app on all your devices. Your data never leaves your infrastructure. Your conversations stay yours [3].

At this point, you've completed the core "Access From Anywhere" setup:

- ✅ Open WebUI running via Docker
- ✅ Tailscale for secure remote access
- ✅ PWA installed on your devices

**From here, you might want to explore:**

- **Features**—discover what Open WebUI can actually do (RAG, model evaluation, tools, and more)
- **Connecting additional models**—add more backends or switch between local and cloud models
- **Evaluation**—figure out which models work best for *your* use cases [3]

Your AI. Your devices. Anywhere you go.