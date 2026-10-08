---
title: "Semi-Automate Copy-to-Clipboard Case Study"
date: "2024-02-08T20:26:58-05:00"
url: "/2024/02/08/semiautomate-copytoclipboard-case-study/"
type: "post"
feed_id: "http://webology.micro.blog/2024/02/08/semiautomate-copytoclipboard-case-study/"
categories: ["Django"]
---

A "copy-to-clipboard" automation is a web page with many formatted text and links that are easy to copy and paste into another application.

My list of links will come from a database, CSV file, JSON file, frontmatter, or a third-party API, depending on what kind of project I am building out.
Once I have my list of links, my automation builds a nicely formatted message based on my link and a text template I write.

For [Django News](https://django-news.com), I automate writing our weekly tweets for social media using this technique.
Each newsletter has a title, issue, and description stored in our database, and I use a template like this snippet to build out our weekly announcements.

```html
{% raw %}
🎉 The Django News Newsletter {{ object.issue }}

{{ object.issue.description }}

[django-news.com/issues/](https://django-news.com/issues/){{ object.issue.number }}#start
{% endraw %}
```

The result, once published on Mastodon, looks like this: [mastodon.social/@djangone...](https://mastodon.social/@djangonews/111822690418364462)

## Copy-to-Clipboard v2

My v2 innovation was adding the [clipboard.js](https://clipboardjs.com/) JavaScript library to press a button to copy the formatted text to my clipboard instead of selecting all of the text so that I could then copy all of the text inside the text box.

I recently added the [elastic-textarea](https://github.com/cloudfour/elastic-textarea) web component, which resized the text box to grow or shrink around my formatted messages.

## DjangoCon US

For DjangoCon US, we built several copy-to-clipboard pages, which build messages to announce talks on [social media](https://2023.djangocon.us/speaking/twitter/) and later help build the metadata we use in our [YouTube videos](https://www.youtube.com/playlist?list=PL2NFhrDSOxgX41jqYSi0HmO9Wsf6WDSmf).
