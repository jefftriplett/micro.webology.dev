---
title: "How I Use django-simple-nav for Dashboards, Command Palettes, and More"
date: "2026-02-26T21:56:51-05:00"
url: "/2026/02/26/how-i-use-djangosimplenav-for/"
type: "post"
feed_id: "http://webology.micro.blog/2026/02/26/how-i-use-djangosimplenav-for/"
categories: ["Django", "Python"]
---

I first got exposed to [django-simple-nav](https://github.com/westerveltco/django-simple-nav) while working with [Josh Thomas](https://github.com/joshuadavidthomas) at [the Westervelt Company](https://github.com/westerveltco) over the last two or three years. It quickly became a go-to library in my toolkit. django-simple-nav lets you define nav items and groupings in Python, then hand them off to a Django template to render. I use it for sidebars, headers, dashboards, and other spots where I need a menu.

Since then, I have also started using it on a lot of personal projects. It has been a great fit every time.

## Defining nav items once and reusing them everywhere

Recently I wanted to reuse parts of a menu nav without having to update a bunch of different files. I had a dashboard with a sidebar full of links, and I also wanted a command palette that could search across all those same options when you hit Command-K from any page. django-simple-nav was a natural fit because you define your items once in Python and render them with whatever template you want.

Here is an example of what that looks like in Python:

```python
from django_simple_nav.nav import Nav
from django_simple_nav.nav import NavGroup
from django_simple_nav.nav import NavItem

NAV_ITEMS = [
    NavItem(title="Home", url="home"),
    NavItem(title="Dashboard", url="dashboard"),
    NavGroup(
        title="Admin & Tools",
        items=[
            NavItem(title="Admin", url="admin:index", permissions=["is_staff"]),
        ],
    ),
    NavItem(title="Login", url="login"),
    NavItem(title="Logout", url="logout"),
]


class DashboardNav(Nav):
    template_name = "nav/dashboard.html"
    items = NAV_ITEMS


class CommandPaletteNav(Nav):
    template_name = "nav/command_palette.html"
    items = NAV_ITEMS

```
## Flexible URLs and named routes

A few things to notice here. When you create a nav item and you have a URL, you can either use the URL's name or you can give it the path to it and it will figure out what it is. So if I want a nav item for the Django admin, I can use `"admin:index"` as the URL.

## Handling permissions without template logic

Another nice feature is the `permissions` parameter. The Admin link uses `permissions=["is_staff"]`, which means it only shows up for staff users. You can use this to hide things based on whether someone is staff, a superuser, or has specific Django permissions. This makes it nice to keep all of your nav options in one place without having to write special conditional logic in your templates to show or hide items for different users.

## Rendering a dashboard nav with Django templates

The other thing to notice is the two Nav classes at the bottom: `DashboardNav` and `CommandPaletteNav`. They both use the same `NAV_ITEMS` list but point to different templates. This is where the reuse really shines.

Here is an example nav template at `templates/nav/dashboard.html`:

```html
<nav>
  {% for item in items %}
    {% if item.items %}
      <span>{{ item.title }}:
        {% for subitem in item.items %}
          <a href="{{ subitem.url }}"{% if subitem.active %} class="active"{% endif %}>
            {{ subitem.title }}
          </a>
        {% endfor %}
      </span>
    {% else %}
      <a href="{{ item.url }}"{% if item.active %} class="active"{% endif %}>
        {{ item.title }}
      </a>
    {% endif %}
  {% endfor %}
</nav>
```
Then in your base template, you can render it with the template tag:

```html
{% load django_simple_nav %}

{% django_simple_nav "myapp.nav.DashboardNav" %}
```
## Building a command palette from the same nav items

Because the `CommandPaletteNav` class uses the same `NAV_ITEMS` list but with a different template, we can render the same nav data as JSON for a command palette. Here is an example template at `templates/nav/command_palette.html`:

```html
{% load django_simple_nav %}

<script type="application/json" id="command-palette-data">
[{% for item in items %}{% if item.items %}{% for subitem in item.items %}
  {"title": "{{ subitem.title }}", "url": "{{ subitem.url }}", "group": "{{ item.title }}"}{% if not forloop.last or not forloop.parentloop.last %},{% endif %}{% endfor %}{% else %}
  {"title": "{{ item.title }}", "url": "{{ item.url }}"}{% if not forloop.last %},{% endif %}{% endif %}{% endfor %}
]
</script>
```
This also lent itself well when I was trying to do something quickly with Claude. I don't know how to build a command palette, but I was able to just have Claude create one. I asked it to use HTMX to keep everything pretty lightweight.

## Final thoughts

All in all, django-simple-nav is a nice library to have in your toolkit. I like using it for headers, menus, dashboard navigation links, and even footer text. If you need flexible, reusable navigation in Django, give it a look.

---

Written by Jeff. Edited with [Grammarly](https://grammarly.com) and [Claude Code](https://claude.ai/code).
