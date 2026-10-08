---
title: "🔋 My django-startproject project updates"
date: "2024-05-26T11:12:26-05:00"
url: "/2024/05/26/my-djangostartproject-project-updates/"
type: "post"
feed_id: "http://webology.micro.blog/2024/05/26/my-djangostartproject-project-updates/"
categories: ["Django"]
---

This morning, I updated my [django-startproject](https://github.com/jefftriplett/django-startproject) to keep up with the latest Django, Docker Compose, ruff, pre-commit, and other versions. This project includes the bare minimum number of batteries I use in my Django projects. 

I also included a justfile, some common recipes, and workflows I use in my personal and client projects. I usually start with these recipes, and then I customize them for the project and the client. 

While these batteries and workflows work for me, I think there is something to be said for starting with Django's default [project_template](https://github.com/django/django/tree/main/django/conf/project_template) and [app_template](https://github.com/django/django/tree/main/django/conf/app_template) to create your own opinionated startproject and startapp templates. 

Create your own start* templates and check out what other people are building. You might learn something that changes your perspective or saves you time.
