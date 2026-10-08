---
title: "🐳 Using Just and Compose for interactive Django and Python debugging sessions"
date: "2024-06-30T09:00:00-05:00"
url: "/2024/06/30/using-just-and-compose-for/"
type: "post"
feed_id: "http://webology.micro.blog/2024/06/30/using-just-and-compose-for/"
categories: ["Django", "Python", "Justfiles", "Docker", "Today I Learned"]
aliases: ["/2024/06/30/using-just-and.html"]
---

When I wrote REST APIs, I spent weeks and months writing tests and debugging without looking at the front end. It's all JSON, after all. 

For most of my projects, I will open two or three tabs. I'm running Docker Compose in tab one to see the logs as I work. I'll use the following [casey/just](https://github.com/casey/just) recipe to save some keystrokes and to standardize what running my project looks like:

```shell
# tab 1
$ just up 
```

In my second tab, I'll open a shell that is **inside** my main web or app container so that I can interact with the environment, run migrations, and run tests. 

We can nitpick the meaning of "console" here, but I tend to have another just recipe for "shell" which will open a Django shell using shell_plus or something more interactive: 

```shell
# tab 2
$ just console
```

In my third tab, I'll run a shell session for creating git branches, switching git branches, stashing git changes, and running my linter, which I prefer to run by hand. 

```shell
# tab 3
$ echo "I'm boring"
```

Over the last year or two, the web has returned to doing more frontend work with Django and less with REST. Using `ipdb`, in my view, to figure out what's going on has been really helpful. Trying to get `ipdb` to "just work" takes a few steps in my normal workflow. 

```
# tab 1 (probably)

# start everything
$ just start

# stop our web container
$ just stop web

# start our web container with "--service-ports" 
# just start-web-with-debug
```

The only real magic here is using Docker's `--service-ports`, which opens ports so we may connect to the open `ipdb` session when we open one in our view code. 


My main `justfile` for all of these recipes/workflows looks very similar to this: 

```yml
# justfile
set dotenv-load := false

@build *ARGS:
    docker compose build {{ ARGS }}

# opens a console
@console:
    docker compose run --rm --no-deps utility/bin/bash

@down:
    docker compose down

@start *ARGS:
    just up --detach {{ ARGS }}

@start-web-with-debug:
    docker compose run --service-ports --rm web python -m manage runserver 0.0.0.0:8000

@stop *ARGS:
    docker compose down {{ ARGS }}

@up *ARGS:
    docker compose up {{ ARGS }}
```

If you work on multiple projects, I encourage you to find patterns you can scale across them. Using Just, Make, shell scripts or even Python lightens the cognitive load when switching between them.
