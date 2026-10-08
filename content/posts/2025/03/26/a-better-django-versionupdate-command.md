---
title: "🤖 A better Django version/update command and Prompt-driven-development"
date: "2025-03-26T19:27:39-05:00"
url: "/2025/03/26/a-better-django-versionupdate-command/"
type: "post"
feed_id: "http://webology.micro.blog/2025/03/26/a-better-django-versionupdate-command/"
categories: ["Django", "Python", "LLM", "UV"]
---


Late last year, I wrote [`django-cli-no-admin,`](https://github.com/jefftriplett/django-cli-no-admin) a proof-of-concept Python library whose goal was to shorten Django's default `django-admin` command to just `django`. 

I published the [package on pypi](https://pypi.org/project/django-cli-no-admin/) and it helped create one of the more colorful [forum topics](https://forum.djangoproject.com/t/name-the-main-command-django/37230) of 2024. I ended up writing two blog posts about it:


- [New project to shorten django-admin to django because we are not monsters](/2024/12/14/new-project-to-shorten-djangoadmin/)
- [🤔 Rethinking Django's Command-Line Tool: Why We Should Rename `django-admin`](/2025/01/08/rethinking-djangos-commandline-tool-why/)


Ever since I had this idea, the idea of building a better `django` command has stuck with me. While I don't see Django embracing the idea, of shortening its default command any time soon, that doesn't mean we shouldn't 


Lately, I have been doing a lot of vibe coding, and I took some inspiration from the [claude-code](https://github.com/anthropics/claude-code)'s cli app, which has a nice developer experience (DX). The claude-code app is version-aware and can query npm's servers to see if a newer version is out and can even update itself. 


I took the output of a few of claude-code's commands and fed that back into Claude and I asked it to build a `django` command that can mimic this behavior with Django using either pip or UV and the PyPI servers to query for the latest Django version.


Here is what the output of my 2-minute vibe coding sessions resulted in or what I prefer to call Prompt-driven-development (PDD): 


```
$ django --version
5.1.6


$ django update
Current version: 5.1.6
Checking for updates...
New version available: 5.1.7 (current: 5.1.6)
Installing update...
Successfully updated from 0.5.1.6 to version 0.5.1.7
```
This just worked on the first try. I used a few follow-up prompts to make it less generic and to default to only ever checking Django. 


One of my favorite features of prompt-driven development is that I create output like this and give it to Claude or ChatGPT, along with a few libraries with which I want to build a new tool. It gives me the working code back in seconds. 


It's incredibly powerful to focus on the end result without worrying about a clever solution and getting lost along the way. With vibe coding or prompt-driven development, we skip the journey and focus on a better result at our destination. 


## What about funding?


I noticed while updating another npm-based project today that it told me that two projects could be funded. 


The Python Packaging User Guide lists `sponsor` in their [Well-known labels](https://packaging.python.org/en/latest/specifications/well-known-project-urls/#well-known-labels) which gives us a data point we could use to list all of the projects that may be funded that we have installed within our Django and/or Python application. 


We could also be baked into our `django` command to determine fundable projects. 


## Thinking outside the box


Simon Willison's LLM command also ships with the ability to update itself and even install [its own plugins](https://llm.datasette.io/en/stable/setup.html#installing-plugins) by wrapping PIP or UV or whatever magic Simon thought up. 


I don't hate using a DX like `django install {package}` to install a new package into my application. It would be really cool if we could even add the package into `INSTALLED_APPS` and make some other suggestion changes if the package could be installed in our urls.py or even explore optional settings that the package might support. I suspect this could even be locally LLM-driven if we wanted to test our docs. 


I also recommend you check out Brett Cannon's [python-launcher](https://github.com/brettcannon/python-launcher) app, a Python library wrapper. Brett was writing Rust wrappers to improve Python tooling before it was popular.
