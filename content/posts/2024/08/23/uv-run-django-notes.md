---
title: "📓 UV Run Django Notes"
date: "2024-08-23T07:45:00-05:00"
url: "/2024/08/23/uv-run-django-notes/"
type: "post"
feed_id: "http://webology.micro.blog/2024/08/23/uv-run-django-notes/"
categories: ["Django", "Python", "UV", "Today I Learned"]
---

I wanted to know how hard it would be to turn one of my [django-startproject](https://github.com/jefftriplett/django-startproject) projects into a `uv run` friendly project. As it turns out, it worked, and the steps were more than reasonable.
## Before the PEP 723'ing...

I started with a fairly vanilla `manage.py` that Django will give you after running `python -m manage startproject`.

```python
"""Django's command-line utility for administrative tasks."""

import os
import sys


def main():
    """Run administrative tasks."""
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "config.settings")
    try:
        from django.core.management import execute_from_command_line
    except ImportError as exc:
        raise ImportError(
            "Couldn't import Django. Are you sure it's installed and "
            "available on your PYTHONPATH environment variable? Did you "
            "forget to activate a virtual environment?"
        ) from exc
    execute_from_command_line(sys.argv)


if __name__ == "__main__":
    main()
```
## shebang

Then we add `#!/usr/bin/env -S uv run` to the top of our `manage.py` file. 

Next, we make our `manage.py` executable and try to run it.

```shell
$ chmod +x manage.py
$ ./manage.py
ModuleNotFoundError: No module named 'django'
```
Our script ran, but Python couldn't find Django. To tell our script to install Django, we can use `uv add—- script` to add it. 

```shell
$ uv add --script manage.py django
Updated `manage.py`
$ ./manage.py
...

Type 'manage.py help <subcommand>' for help on a specific subcommand.

Available subcommands:

[django]
    check
    compilemessages
    createcachetable
    dbshell
    diffsettings
    dumpdata
    flush
    inspectdb
    loaddata
    makemessages
    makemigrations
    migrate
    optimizemigration
    runserver
    sendtestemail
    shell
    showmigrations
    sqlflush
    sqlmigrate
    sqlsequencereset
    squashmigrations
    startapp
    startproject
    test
    testserver
Note that only Django core commands are listed as settings are not properly configured (error: No module named 'environs').
```
Django worked as expected this time, but Python could not find a few third-party libraries I like to include in my projects.

To add these, I passed the other four to `uv add --script` which will add them to the project.

```shell
$ uv add --script manage.py django-click "environs[django]" psycopg2-binary whitenoise
Updated `manage.py`
...
$ ./manage.py
...
```
Our Django app's `manage.py` works when we run it. 

## After the PEP 723'ing...

After we installed our dependencies in our `manage.py` file, they were added to the top of the file between the `///` blocks.

```python
#!/usr/bin/env -S uv run
# /// script
# requires-python = ">=3.10"
# dependencies = [
#     "django",
#     "django-click",
#     "environs[django]",
#     "psycopg2-binary",
#     "whitenoise",
# ]
# ///
"""Django's command-line utility for administrative tasks."""

import os
import sys


def main():
    """Run administrative tasks."""
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "config.settings")
    try:
        from django.core.management import execute_from_command_line
    except ImportError as exc:
        raise ImportError(
            "Couldn't import Django. Are you sure it's installed and "
            "available on your PYTHONPATH environment variable? Did you "
            "forget to activate a virtual environment?"
        ) from exc
    execute_from_command_line(sys.argv)


if __name__ == "__main__":
    main()
```
