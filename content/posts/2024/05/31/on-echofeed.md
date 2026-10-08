---
title: "📝 On EchoFeed"
date: "2024-05-31T17:59:52-05:00"
url: "/2024/05/31/on-echofeed/"
type: "post"
feed_id: "http://webology.micro.blog/2024/05/31/on-echofeed/"
categories: ["Django", "Today I Learned"]
aliases: ["/2024/05/31/on-echofeed.html"]
---

[EchoFeed](https://echofeed.app) is a cheap ($20 to $25 a year) and simple service that takes an RSS, Atom, or JSON feed and posts it to a half dozen services like Mastodon, Micro.blog, Bluesky, and even Discord.

The service also supports GitHub, [Webmentions](https://help.echofeed.app/services/#webmentions), and [Webhooks](https://help.echofeed.app/services/#web-request-webhook), opening up many exciting possibilities. 

What makes the service interesting is its support of [variables](https://help.echofeed.app/variables/), making creating a template for your posts possible. 

I found this feature helpful for templating job listings for [Django News Jobs](https://jobs.django-news.com) updates to include hashtags and for weekly [Django News Newsletter](https://django-news.com) release posts. 

EchoFeed is a useful service to help wire up static projects and a nice stopgap until more apps support the Fediverse.
