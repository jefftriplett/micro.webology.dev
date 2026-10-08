---
title: "Python Click, django-click, and Typer notes"
date: "2025-01-22T19:37:45-05:00"
url: "/2025/01/22/python-click-djangoclick-and-typer/"
type: "post"
feed_id: "http://webology.micro.blog/2025/01/22/python-click-djangoclick-and-typer/"
categories: ["Django", "Python", "Today I Learned"]
---



One of the most significant Python innovations in my development toolchain was the [Click](https://click.palletsprojects.com) utility, which simplified the creation of Python scripts. Click changed how I approach writing one-off Python scripts and made it easier for me to write better developer experiences around those scripts. 


Once I found [django-click](https://github.com/GaretJax/django-click), writing Django management commands was a breeze, using the same Click API that I was already familiar with. 


Arguably, the second most significant innovation was the [Typer](https://typer.tiangolo.com) library, built on Click, making writing Python scripts even easier. I didn't think it was possible to be easier than Python Click until Typer came out and proved me wrong. 


## The Python Click library


A typical pattern I use with Click is creating a command that accepts an argument like a URL. 


```python
import click


@click.command()
@click.argument("url", type=str)
def command(url):
	do_something(url=url)
```
## The Python django-click library


This works well, but one improvement would be to accept as many `url` arguments as I can pass to it. Thankfully, Click solves this with the `nargs` argument. I always have to look this up, which is why we are here.  


```python
import djclick as click


@click.command()
@click.argument("urls", nargs=-1, type=str)
def command(urls):
    for url in urls:
        do_something(url=url)
```
## The Python Typer library


Suppose we were writing this example with Typer. In that case, we could simplify it to using Python's native data types, which would make it feel more like I'm writing native code and less like I'm using a library.


```python
import typer


app = typer.Typer() 


@app()
def command(urls: list[str]): 
    for url in urls:
        do_something(url=url)
```
## Conclusion


There is also a [django-typer](https://github.com/django-commons/django-typer) library, bringing the Typer library to Django. I suspect I'll switch to django-typer the next time I start a new project to give it a good test drive. I can speculate on what that looks like, but I'll leave that for another day.
