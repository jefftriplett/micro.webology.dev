---
title: "New project to shorten django-admin to django because we are not monsters"
date: "2024-12-14T22:18:43-05:00"
url: "/2024/12/14/new-project-to-shorten-djangoadmin/"
type: "post"
feed_id: "http://webology.micro.blog/2024/12/14/new-project-to-shorten-djangoadmin/"
categories: ["Django", "Python"]
aliases: ["/2024/12/14/new-project-to.html"]
---

One of the biggest mysteries in Django is why I have to run `django-admin` from my terminal instead of just running `django`. Confusingly, `django-admin` has nothing to do with Django's admin app. 

If you have ever wondered why and wanted to type `django` from your terminal, my new project, `django-cli-no-admin` solves this problem for you. 

I looked at several package names on [PyPI](https://pypi.org), including `django-cli`, which I liked the best (someone is name squatting this package.)

I gave up and went with [`django-cli-no-admin`](https://pypi.org/project/django-cli-no-admin/) for lack of a better name. 

```shell
# new school
uv pip install django-cli-no-admin

# old school
pip install django-cli-no-admin

# to use it...
django --version 
```
This tool aliases Django's `django-admin` script does but we shorted the name by 50%: 


```toml
[project.scripts]
django = "django.core.management:execute_from_command_line"
```
## Should Django adopt this? 

Yes. But we can leave `django-admin` alone since we have ~20 years of history referencing it. 

## How long has this lived in your head?

Almost two decades. 

## Where is the code? 

https://github.com/jefftriplett/django-cli-no-admin
