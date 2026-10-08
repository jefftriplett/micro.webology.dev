---
title: "🚜 On Evolving Django's `auth.User` model"
date: "2024-09-10T12:31:48-05:00"
url: "/2024/09/10/on-evolving-djangos-authuser-model/"
type: "post"
feed_id: "http://webology.micro.blog/2024/09/10/on-evolving-djangos-authuser-model/"
categories: ["Django", "Today I Learned"]
---

I need to re-read/re-listen to Carlton's [Evolving Django's `auth.User`
](https://buttondown.com/carlton/archive/evolving-djangos-authuser/) Stack Report before I have a firm opinion, but I saw his [Mastodon post](https://mastodon.social/@carlton@fosstodon.org/113113728832109272) and I thought it was worth sharing some initial thoughts. 


On my first read, I fell into the camp that wants `django-unique-user-email` and full name to be the defaults on Django's built-in User. I have wanted this forever, and my clients do, too.


Django should still allow me to create a custom user, but the documentation could be better. Django's documentation is a topic for another day, but I'm confused by it and find it less and less helpful. I notice the developers I work with get lost in them, too. Docs may be a good DjangoCon US topic if you want to discuss it in a few weeks. 


I would love the default User to have a unique email address, full name, and a short name. Optionally, a username is an email address setting. Please don't take away the ability to have a custom User model. (**Update:** Carlton is *not* making a case for removing a custom User model, but others have made that argument. No, thank you.) 


Carlton's "Action points" conclusion seems reasonable to me.
