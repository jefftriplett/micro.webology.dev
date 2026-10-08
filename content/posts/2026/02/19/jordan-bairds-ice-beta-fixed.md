---
title: "Jordan Baird's Ice beta fixed my macOS Tahoe menu bar issues"
date: "2026-02-19T09:00:00-05:00"
url: "/2026/02/19/jordan-bairds-ice-beta-fixed/"
type: "post"
feed_id: "http://webology.micro.blog/2026/02/19/jordan-bairds-ice-beta-fixed/"
summary: "Jordan Baird’s Ice is an open-source app that effectively manages macOS menu bar icons, and a recent beta version resolved a color issue after upgrading to macOS Tahoe."
categories: ["Today I Learned"]
---

If you use a Mac, you've probably noticed that the menu bar fills up with icons pretty quickly. [Bartender](https://www.macbartender.com) and [Ice](https://github.com/jordanbaird/Ice) (sadly, now an unfortunate name) are apps that let you manage and hide unwanted icons from your macOS menu bar so it stays clean and uncluttered.

About a year ago, I switched from Bartender to Ice, which just happens to be open source, because there was [some drama](/2024/06/04/bartender-mac-app.html). Since then, I've been very happy with Ice.

A couple of months ago, I upgraded to macOS Tahoe, and my menu bar stopped working correctly. The icon colors were all this weird shade of blue, so I couldn't customize anything. After months of trying to figure it out, I noticed that it had been a while since Ice released a new version. That's how open source goes sometimes.

I was getting to the point of deciding whether to go back to Bartender or stick with Ice. Today, I noticed that there's a Homebrew package for `jordanbaird-ice@beta`. I decided to give it a try, removed the old version, installed the beta, and to my surprise and delight, the problem was fixed.

```shell
# remove the stable version
brew remove jordanbaird-ice

# install the beta
brew install jordanbaird-ice@beta
```
I'm hoping there's a more official release soon. The new Bartender looks good too, so if Ice doesn't keep getting updated, I might switch back. If you've run into this same issue, give the beta a try and let me know how it goes. And if you know of any alternatives to Bartender and Ice, I'd love to hear about those too.
