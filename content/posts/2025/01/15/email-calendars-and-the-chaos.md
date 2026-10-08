---
title: "📩 Email, Calendars, and the Chaos of Modern Workflows"
date: "2025-01-15T21:51:45-05:00"
url: "/2025/01/15/email-calendars-and-the-chaos/"
type: "post"
feed_id: "http://webology.micro.blog/2025/01/15/email-calendars-and-the-chaos/"
categories: ["Django", "Python", "Today I Learned"]
---

I was feeling overloaded with emails this week, and then I remembered that my out-of-office auto-responder told people they should contact me after the first of the year if they needed me to reply. 


Thankfully, I could select and archive all of my 2024 emails with this rule `label:inbox after:2023/12/31 before:2025/01/01`, which reconciled my old emails. 


## Calendars and shared Documents 


With each Google organization, I'm a member with another Google Calendar, Google Drive, and Google Contacts to manage. That document someone wants feedback on sometimes feels like spinning a wheel, and I need to guess which inbox and account the message might land in. 


The best solution that I have found for juggling meeting invites is [Reclaim](https://reclaim.ai), which is terrific for merging multiple calendars into one calendar so I can at least keep on top of meeting invites and scheduling. Dropbox recently bought them, but I'm hoping that Dropbox will leave them alone. 


Email and calendars have become more challenging since I switched to a Mac Studio at the office. While we were returning to work during a blizzard last week, I realized that my personal Mac Mini in my home office had no concept of my work calendar or the 4 or 7 Vivaldi profiles with syncing that I use to jump between orgs all day. 


With 1Password, this is a straightforward process to set up and authorize, but it still takes time. 


Tonight, I'm pretty sure I even locked myself out of one service because it's probably not a typical usage pattern to jump between three Macs over two locations with a half dozen profiles to juggle. 


## Calendar Agent


Over the Thanksgiving break, I wrote my first Calendar Agent, who can read and write to my work calendar. It's not fully baked yet, but it works well enough to tell me about my upcoming meetings and to create a meeting for me. Sometimes. 


The biggest downside to using my Calendar Agent is that I have to run it from my terminal, which isn't always the most convenient place. 


Side note: I might rewrite my agent using [PydanticAI](https://ai.pydantic.dev) as an excuse to learn about the Python agent framework, streamline tool-calling, and play with more local agents using [Ollama](https://ollama.com). 


## The better email solution


The better email solution was a Django email app called Concorde, one of [Adam Fast](https://github.com/adamfast)'s creations. It was Django querysets for managing email rules, which I modified and ran over the years. It quickly created better rules than Gmail supported, like deleting old messages in specific folders after x-days. When I kept my fork running and updated, the tool was invaluable. When I kept my Concorde up and running, my email life was healthier than when I was slower to fix it after an upgrade. 


## Conclusion


I'm annoyed that the best solutions for these problems are to either pay a company to make a Google Suite usable or you must be a developer to build tools to manage it all. 


This stuff sucks.
