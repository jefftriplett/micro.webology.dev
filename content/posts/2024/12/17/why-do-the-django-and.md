---
title: "🤷 Why do the Django and Python communities use so many Google Forms? "
date: "2024-12-17T12:09:32-05:00"
url: "/2024/12/17/why-do-the-django-and/"
type: "post"
feed_id: "http://webology.micro.blog/2024/12/17/why-do-the-django-and/"
categories: ["Django", "Python"]
aliases: ["/2024/12/17/why-do-the.html"]
---

Last week, I wrote but didn't publish some notes about why the Django and Python communities use so many Google Forms. 


The simple answer is that Google Forms are quick and easy to set up, and data can be easily exported via Google Sheets or a CSV file. 


Getting data in and out of Django isn't hard, but why isn't it as easy as using Google Forms? 


I'd love to see a Django version of Google Forms that we can all use. 


Has anyone solved this problem?


From a technical perspective, Django ships with a `JSONField`, which can store any form data we want without having to migrate databases. Turning a flat `JSONField` into CSV is already a solved problem. 


**Please note:** I am not looking for a Django forms wrapper or your opinions about why Django should use your fancy Django forms tool.
