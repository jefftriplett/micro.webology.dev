---
title: "🐳 Managing Docker Compose Profiles with Just: Switching Between Default and Celery Configurations"
date: "2024-06-25T22:10:38-05:00"
url: "/2024/06/25/managing-docker-compose-profiles-with/"
type: "post"
feed_id: "http://webology.micro.blog/2024/06/25/managing-docker-compose-profiles-with/"
categories: ["Justfiles", "Docker"]
aliases: ["/2024/06/25/managing-docker-compose.html"]
---

For a recent client project, we wanted to toggle between various Docker Compose profiles to run the project with or without Celery. 

Using Compose's `profiles` option, we can label services that we may not want to start by default a label. This might look something like this:

```yaml
services:

  beat:
    profiles:
      - celery
    ...

  celery:
    profiles:
      - celery
    ...


  web:
    ...
```


We use a [casey/just](https://github.com/casey/just) justfile for some of our common workflows, and I realized I could set a `COMPOSE_PROFILES` environment variable to switch between running a "default" profile and a "celery" profile. 

Using just's [`env_var_or_default`](https://github.com/casey/just?tab=readme-ov-file#environment-variables) feature, we can set both an ENV variable and a default value to fall back on for our project. 

```bash
# justfie 

export COMPOSE_PROFILES := env_var_or_default('COMPOSE_PROFILES', 'default')

@up *ARGS:
    docker compose up {{ ARGS }}

# ... the rest of your justfile...

```

To start our service *without Celery*, I would run:

```bash
$ just up
```
`
To start our service *with Celery*, I would run:

```bash
$ export COMPOSE_PROFILES=celery
$ just up
```

Our `COMPOSE_PROFILES` environment variable will get passed into our `just up` recipe, and if we don't include one, it will have a default value of `default`, which will skip running the Celery service.
