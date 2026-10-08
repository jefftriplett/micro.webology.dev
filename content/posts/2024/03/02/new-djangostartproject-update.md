---
title: "New `django-startproject` update"
date: "2024-03-02T23:27:42-05:00"
url: "/2024/03/02/new-djangostartproject-update/"
type: "post"
feed_id: "http://webology.micro.blog/2024/03/02/new-djangostartproject-update/"
categories: ["Django", "Python"]
---

I updated my [`django-startproject`](https://github.com/jefftriplett/django-startproject) project today to support the latest versions of Django, Python, Compose, and other tools I'm a fan of. I use `django-startproject` to spin up projects that need some batteries quickly, but not every battery. 

Features: 
- Django 5.0
- Python 3.12
- Docker Compose 3
- Adds [casey/just](https://github.com/casey/just) recipes/workflows (Just is a command runner, not a build tool)
- Adds [uv](https://github.com/astral-sh/uv) support 

`uv` is the newest addition, which is a Python package installer and [pip-tools](https://github.com/jazzband/pip-tools/) replacement. It's not a 100% drop-in replacement for pip and pip-tools, but it cuts my build times in half, and I have yet to hit any significant show-stoppers.
