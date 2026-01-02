# Setting Up Tailscale with Open WebUI

## Why Tailscale?

You've got Open WebUI running at home. It works great—when you're home. But what about when you're at a coffee shop? On your phone during a commute? At the office?

You _could_ expose your instance to the public internet. Port forwarding, dynamic DNS, SSL certificates, security hardening... or you could not do any of that.

Tailscale creates a private network between your devices. Your laptop, your phone, your tablet, your server—they all talk to each other like they're on the same WiFi, no matter where they actually are. No open ports. No public IP. No exposure to the internet at large.

The result: you can access your Open WebUI instance from anywhere in the world, on any of your devices, without exposing it to anyone else.

### TL;DR

- **What this does**: Secure access to Open WebUI from anywhere—laptop, tablet, phone—without exposing it to the internet
- **What you need**: A Tailscale account (free), the standard Docker setup for Open WebUI, about 15 minutes
- **What you get**: HTTPS access via a private URL only your devices can reach, automatic login using your Tailscale identity

---

## How Does This Work?

Tailscale runs as a "sidecar" container alongside Open WebUI. It joins your personal Tailscale network and handles all the networking—encryption, certificates, the works.

Your Open WebUI instance gets a private hostname like `open-webui.tail1234.ts.net`. That URL only works from devices signed into _your_ Tailscale account. Anyone else? They can't even see it exists.

Even better: Tailscale can pass along _who's_ connecting, so Open WebUI knows it's you without needing a separate login.

---

## Before You Start

This guide assumes you're running Open WebUI using Docker, following the recommended setup from the docs. If you're running it some other way, the concepts still apply, but the specifics will differ.

You'll need:

- A [Tailscale account](https://tailscale.com/) (free tier is plenty)
- Docker and Docker Compose installed
- Open WebUI already running (or ready to set up)

---

## Step 1: Create a Tailscale Account and Install on Your Devices

If you haven't already, sign up at [tailscale.com](https://tailscale.com/).

Then install Tailscale on the devices you want to use:

- **Phone**: Download from the App Store (iOS) or Play Store (Android)
- **Laptop/Desktop**: [Download for your OS](https://tailscale.com/download)

Sign in on each device. That's it—they're now on your private network.

---

## Step 2: Generate an Auth Key

Your Open WebUI server needs to join your Tailscale network too. For that, you'll need an auth key.

1. Go to your [Tailscale admin console](https://login.tailscale.com/admin/settings/keys)
2. Click **Generate auth key**
3. Settings to consider:
   - **Reusable**: Your call. A single-use key is more secure, but you'll need a new one if you ever redeploy.
   - **Ephemeral**: Probably leave this off—you want this node to stick around.
   - **Tags**: If you want to use access controls later, add something like `tag:open-webui`. (Optional for now.)

4. Copy the key somewhere safe. You'll need it in a moment.

---

## Step 3: Create the Tailscale Configuration

Tailscale needs to know how to route traffic to Open WebUI. Create a folder called `tailscale` and add this file:

```json title="tailscale/serve.json"
{
	"TCP": {
		"443": {
			"HTTPS": true
		}
	},
	"Web": {
		"${TS_CERT_DOMAIN}:443": {
			"Handlers": {
				"/": {
					"Proxy": "http://open-webui:8080"
				}
			}
		}
	}
}
```

This tells Tailscale: "When someone connects on HTTPS, send them to Open WebUI." The `${TS_CERT_DOMAIN}` part gets filled in automatically with your server's Tailscale hostname.

---

## Step 4: Set Up Docker Compose

Here's the full configuration. If you already have a `docker-compose.yaml` for Open WebUI, you'll be adding the `tailscale` service to it.

```yaml title="docker-compose.yaml"
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    volumes:
      - open-webui:/app/backend/data
    environment:
      - WEBUI_AUTH_TRUSTED_EMAIL_HEADER=Tailscale-User-Login
      - WEBUI_AUTH_TRUSTED_NAME_HEADER=Tailscale-User-Name
    restart: unless-stopped

  tailscale:
    image: tailscale/tailscale:latest
    environment:
      - TS_AUTH_ONCE=true
      - TS_AUTHKEY=${TS_AUTHKEY}
      - TS_EXTRA_ARGS=--advertise-tags=tag:open-webui
      - TS_SERVE_CONFIG=/config/serve.json
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_HOSTNAME=open-webui
    volumes:
      - tailscale:/var/lib/tailscale
      - ./tailscale:/config
      - /dev/net/tun:/dev/net/tun
    cap_add:
      - net_admin
      - sys_module
    restart: unless-stopped

volumes:
  open-webui: {}
  tailscale: {}
```

### What's all this?

| Setting                           | What it does                                                                   |
| --------------------------------- | ------------------------------------------------------------------------------ |
| `TS_AUTHKEY`                      | Authenticates your server to your Tailscale network                            |
| `TS_HOSTNAME`                     | The name your server gets—you'll access it at `open-webui.your-tailnet.ts.net` |
| `TS_SERVE_CONFIG`                 | Points to the config file you created                                          |
| `WEBUI_AUTH_TRUSTED_EMAIL_HEADER` | Tells Open WebUI to trust the identity Tailscale provides                      |
| `cap_add` and `/dev/net/tun`      | Gives Tailscale permission to create the VPN tunnel. Yeah, it needs these.     |

---

## Step 5: Start It Up

Set your auth key as an environment variable and launch:

```bash
export TS_AUTHKEY=tskey-auth-xxxxx-xxxxxxxxxx
docker compose up -d
```

Give it a minute to connect. You can check the logs if you're curious:

```bash
docker logs tailscale
```

Once it's connected, you should see your new node in the [Tailscale admin console](https://login.tailscale.com/admin/machines).

---

## Step 6: Access Open WebUI

From any device signed into your Tailscale account, open:

```
https://open-webui.your-tailnet.ts.net
```

Replace `your-tailnet` with your actual Tailscale network name (you'll find it in the admin console—it's something like `tail1234` or a custom name if you set one).

That's it. You're in. From anywhere.

---

## Setting Up Your Mobile Devices

This is where it gets good. With Tailscale on your phone, you can access Open WebUI from literally anywhere with an internet connection.

### iOS

1. Install [Tailscale from the App Store](https://apps.apple.com/app/tailscale/id1470499037)
2. Sign in with the same account
3. Toggle the connection on

**Want it always connected?** Go to the Tailscale app settings and enable **Always On VPN**. Your phone will automatically connect to your Tailscale network whenever it has internet.

**Hide the VPN icon?** Unfortunately, iOS always shows the VPN indicator when a VPN is active. No way around that one—Apple's rules.

### Android

1. Install [Tailscale from the Play Store](https://play.google.com/store/apps/details?id=com.tailscale.ipn)
2. Sign in with the same account
3. Toggle the connection on

**Always-on connection**: Go to your phone's **Settings → Network & Internet → VPN → Tailscale** (gear icon) → Enable **Always-on VPN**. Now it reconnects automatically.

**Hide the VPN icon?** On some Android versions, you can. Go to **Settings → Notifications → Tailscale** and disable the persistent notification. The key icon in the status bar usually stays, but some manufacturers let you hide it in status bar settings. Worth poking around.

---

## A Note on Security

By default, any device on your Tailscale network can access your Open WebUI instance. If it's just your personal devices, that's probably fine.

But if you've shared your Tailscale network with family, friends, or coworkers, you might want to lock things down. Tailscale has access controls (ACLs) that let you specify exactly who can reach what.

That's a topic for another guide—but if you're curious, check out [Tailscale's ACL documentation](https://tailscale.com/kb/1018/acls/).

---

## Troubleshooting

**Can't reach the URL?**

- Is Tailscale running on the device you're connecting _from_? Check the app.
- Is the server showing up in your [Tailscale admin console](https://login.tailscale.com/admin/machines)?
- Check the container logs: `docker logs tailscale`

**Logged in as the wrong user, or not logged in at all?**

- The automatic login relies on traffic coming through Tailscale Serve. If you're accessing Open WebUI some other way (like directly on your local network), those identity headers won't be there.

**Need to start fresh?**

- Stop the containers: `docker compose down`
- Remove the Tailscale volume: `docker volume rm your-project_tailscale`
- Generate a new auth key and try again

---

## What's Next?

You've got secure, private access to Open WebUI from anywhere. Your traffic never touches the public internet. Your data stays yours [4].

**Ready for the next step?** Now that you've got HTTPS access via Tailscale, you can install Open WebUI as a Progressive Web App (PWA) on your devices. This gives you an app-like experience—home screen icon, fullscreen mode, and offline access when you're on your local network [1].

Check out the **HTTPS Tutorials** section to explore other secure access options [3], or head to the PWA setup guide to get that native app feel on your phone and tablet.

Your network. Your devices. Your AI.
