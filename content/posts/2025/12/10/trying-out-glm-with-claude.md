---
title: "🤖 Trying Out GLM with Claude Code"
date: "2025-12-10T20:43:48-05:00"
url: "/2025/12/10/trying-out-glm-with-claude/"
type: "post"
feed_id: "http://webology.micro.blog/2025/12/10/trying-out-glm-with-claude/"
categories: ["LLM", "Today I Learned"]
---


My friend [Trey Hunner](https://treyhunner.com) showed me the GLM set of models before Thanksgiving. While traveling to see family, I somehow messed up my Claude Code setup because of a wrapper I have with [mise-en-place](https://mise.jdx.dev). I couldn't use it for a while, and that made me realize I really need a backup for Claude Code.

## Why GLM?

[Z.AI](https://z.ai)'s GLM model is better than Gemini but not quite as good as Claude Code. It's really fast (about twice as fast as Claude Code), seems like 90+ percent as good, and it's really cheap. You can get an annual subscription for around $26-28 for the first year, and I've read online that it's very hard to hit the limit even on the lowest tier subscription.

This is a great option for folks who can't quite justify the $100/mo Claude plan but occasionally hit limits on the $20/mo Claude plan. I actually subscribe to the $100/mo plan, but I ended up getting the GLM Pro Plan because I like the amount of usage it gives me. The plan I'm on has five times as much token usage as the base tier.

## Running Both Side by Side

There's a [wrapper tool](https://github.com/JoeInnsp23/claude-glm-wrapper) that lets you use Z.AI's models as Claude Code's backend, so you can run both Claude and Z.AI's GLM in two different windows. Having a reasonable backup that I can switch between or run in parallel is nice.

I never find speed to be an issue with Claude Code, but I'm definitely a fan of having options.

## API Access

Claude doesn't include API key access without paying extra. GLM solves this problem by giving you a raw API for a set price per month. Their API is OpenAI compatible, so I can work on agentic scripts using Open Coder or other applications without paying extra for Anthropic tokens.

## Getting Started

To get started, run:

```bash
bunx claude-glm-installer
```
This will give you bash aliases that let you run various GLM models while still letting Claude default to the Anthropic backend:

```bash
ccg              # Claude Code with GLM-4.6 (latest)
ccg45            # Claude Code with GLM-4.5
ccf              # Claude Code with GLM-4.5-Air (faster)
cc               # Regular Claude Code
```
Trey also told me about [claude-code-router](https://github.com/musistudio/claude-code-router), which lets you change models on the fly without restarting Claude Code. This might work well if you want to switch between models mid-session.

If you find yourself running out of Claude Code tokens a couple of times a week or even a couple of times a day, it might be worth checking out GLM as a backup or alternative.

If you want to try out Z.AI's GLM models, please use [my invite link](https://z.ai/subscribe?ic=GLMN4NLXLV) (affiliate) or feel free to use [Trey Hunner's invite link](https://z.ai/subscribe?utm_medium=edm&utm_content=blackfriday&_channel_track_key=PJg2GPj2) (affiliate) instead.

## Resources

- [Claude GLM Installer tool on Reddit](https://www.reddit.com/r/ClaudeCode/comments/1nv64g5/i_made_a_tool_to_use_zais_glm_models_with_claude/)
- [claude-glm-wrapper on GitHub](https://github.com/JoeInnsp23/claude-glm-wrapper)
- [claude-code-router on GitHub](https://github.com/musistudio/claude-code-router)

---

Written by Jeff. Edited with [Grammarly](https://grammarly.com) and [Claude Code](https://claude.ai/code).
