---
title: "Django Extensions is useful even if you only use show_urls"
date: "2024-07-06T09:00:00-05:00"
url: "/2024/07/06/django-extensions-is-useful-even/"
type: "post"
feed_id: "http://webology.micro.blog/2024/07/06/django-extensions-is-useful-even/"
categories: ["Django", "Python"]
aliases: ["/2024/07/06/django-extensions-is.html"]
---

Yes, [Django Extensions](https://github.com/django-extensions/django-extensions) package is worth installing, especially for its show_urls command, which can be very useful for debugging and understanding your project's URL configurations. 

Here's a short example of how to use it because I sometimes want to include a link to the Django Admin in a menu for staff users, and I am trying to remember what name I need to reference to link to it. 

First, you will need to install it via:

```bash
pip install django-extensions

# or if you prefer using uv like me:
uv pip install django-extensions
```

Next, you'll want to add `django_extensions` to your `INSTALLED_APPS` in your `settings.py` file:

```python
INSTALLED_APPS = [
    ...
    "django_extensions",
]
```

Finally, to urn the `show_urls` management command you may do some by running your `manage.py` script and passing it the following option:

```shell
$ python -m manage show_urls
```

Which will give this output:

```shell
$ python -m manage show_urls | grep admin
...
/admin/	django.contrib.admin.sites.index	admin:index
/admin/<app_label>/	django.contrib.admin.sites.app_index	admin:app_list
/admin/<url>	django.contrib.admin.sites.catch_all_view
# and a whole lot more...
```

In this case, I was looking for `admin:index` which I can now add to my HTML document this menu link/snippet:

```html
... 
<a href="{% url 'admin:index' %}">Django Admin</a>
... 
```

What I like about this approach is that I can now hide or rotate the url pattern I'm using to get to my admin website, and yet Django will always link to the correct one.
