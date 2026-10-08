---
title: "🤖 On GitHub Copilot CLI and prompts as code"
date: "2025-10-04T20:57:19-05:00"
url: "/2025/10/04/on-github-copilot-cli-and/"
type: "post"
feed_id: "http://webology.micro.blog/2025/10/04/on-github-copilot-cli-and/"
categories: ["Django", "Python", "LLM"]
---

I checked out William Vincent's [The Secret Prompts in GitHub Copilot CLI](https://wsvincent.com/copilot-cli-secret-prompts/) tonight, and I wanted to share a few tips and what stood out to me. 

## GitHub Copilot CLI uses Claude Sonnet 4.5 by default

> No luck other than confirming it is using Claude models by default. Apparently, you can change the underlying model, for example, to ChatGPT 5, by updating the environment variable `COPILOT_MODEL=gpt-5`; however, we will work with the defaults here.

You can Copilot CLI's default model via the `/model` command and it will also let you pick between three models. 

```shell
 Select Model

 Choose the AI model to use for Copilot CLI. The selected model will be persisted and used for future sessions.

 ❯ 1. Claude Sonnet 4.5 (default) (current)
   2. Claude Sonnet 4
   3. GPT-5
   4. Cancel (Esc)

 Use ↑/↓ to navigate, Enter to select, Esc to cancel
```
I'm somewhat surprised that GitHub CLI isn't shipping with `gpt-5-codex` model support yet. From my testing, it appears to be OpenAI's best coding model, but it may be shipping soon. 

## The "You are" trick

> Well, what we "really" care about are any prompts that start with "you are" since those are instructions from Copilot CLI to the model.

The "you are" tip is one I shared with Will and [Simon Willison](https://simonwillison.net), which I have used for a few years when trying to find a tool's system prompt, which is always buried and obfuscated in their JavaScript files. 

Simon and I were invited to Microsoft HQ last month for an AI Insider's summit (I prefer not to use the term influencer), where we were given early access to GitHub Copilot CLI before the public release. The first thing we both did was dive into the system prompt to see what it contained. Every system prompt has "You are" buried in it somewhere, which makes it much easier to find that paging through 10k lines of JavaScript. 

## Use Xml tags in your prompts

Will posted the Copilot CLI's system prompt, and one thing that stood out to me was the various XML-tagged sections, such as `<tips_and_tricks>` and `<style>`, which Anthropic has encouraged for years. They documented the technique in the [Use XML tags to structure your prompts](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags) section of their docs. 

## Natural language prompts are becoming the universal programming interface

I have been experimenting with LLMs since the release of GPT-2. While I understand why it pains many developers to admit this, natural language prompts have become a language-agnostic way to program. Somebody could build the same app I'm building using Django with the same prompts in Laravel, Rails, or any other well-documented web framework and underlying programming language. 

For many people who are new to development, this is more obvious: 

> Prompts are code.

Languages like Python aren't going away, but it's much easier and faster to develop when pairing with an LLM assistant who is always online and can instantly answer any questions that you might have. 

The more I examine tools like GitHub Copilot CLI, the clearer it becomes: understanding how these tools prompt their models matters not just for curiosity's sake, but because knowing how the prompt works helps you work better with the tool. Next time you're using an AI coding assistant, use the "You are" trick to peek under the hood. You might be surprised by what you find.
