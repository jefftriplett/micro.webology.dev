---
title: "🤖 VibeOps: Using Claude Code on Cheap VPS Servers"
date: "2025-08-06T19:05:47-05:00"
url: "/2025/08/06/vibeops-using-claude-code-on/"
type: "post"
feed_id: "http://webology.micro.blog/2025/08/06/vibeops-using-claude-code-on/"
categories: ["LLM", "Today I Learned"]
---

Today I came across [Pieter Levels' post](https://x.com/levelsio/status/1953022273595506910) about "VibeOps," a workflow that involves SSHing to a cheap VPS server and installing Claude Code directly on it. I'm running this setup on a cheap Hetzner box. While this approach might sound risky at first, when combined with a secure networking solution like [Tailscale](https://tailscale.com) and properly configured as a Tailnet, it becomes both safe and worth experimenting with.

I've also been exploring a complementary tool called [Vibe Tunnel](https://vibetunnel.sh), which integrates well with Tailscale and my existing Tailnet setup. It provides an elegant way to remotely create or connect to an existing Claude Code session from my browser. I like the idea of letting Claude handle some routine remote tasks.

Security is essential here. My Hetzner box uses their firewall product to block all ports except for SSL (443) and only allows me to access the box via Tailscale. If you aren't using a firewall and a VPN product like Tailscale, you should not use a product like Vibe Tunnel to allow access to a running shell on your servers. 

While trying to install Vibe Tunnel, I ran into a PAM error, so I did what anyone would do with Claude Code available on the server: I let Claude fix it for me. I thought Claude could figure it out, but after 5 to 10 minutes of noble efforts, I found [issue #499](https://github.com/amantus-ai/vibetunnel/issues/499) and [pull request #521](https://github.com/amantus-ai/vibetunnel/pull/521), which point to a bigger issue with a potential fix coming soon. 

While I was on my server, I asked Claude to look at my Caddy setup for a bunch of parked domains, and it found some actionable changes and even fixed a few broken paths that weren't obvious. This is exactly the kind of routine server maintenance where having Claude available directly on the server proves helpful. 

I also had Claude check to see if the machine was out-of-date, and I watched it install a month's worth of updates. Claude even wrote a nice summary for me to share in this post: 

> Analysis: The system is running a current Long Term Support release of Ubuntu with extended support until 2029. All installed packages are current with no pending updates available. No maintenance required at this time.

> Action Taken: System audit only - no changes were made to the system.

All in all, I am a fan, even if I wouldn't recommend this for any clients or just anyone.
