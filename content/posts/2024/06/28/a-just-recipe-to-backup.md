---
title: "🐘 A Just recipe to backup and restore a Postgres database"
date: "2024-06-28T23:58:54-05:00"
url: "/2024/06/28/a-just-recipe-to-backup/"
type: "post"
feed_id: "http://webology.micro.blog/2024/06/28/a-just-recipe-to-backup/"
categories: ["Justfiles", "Docker", "Postgres"]
aliases: ["/2024/06/28/a-just-recipe.html"]
---

I have used this [casey/just](https://github.com/casey/just) recipe to help backup and restore my Postgres databases from my Docker containers. 

I work with a few machines, and it's an excellent way to create a database dump from one machine and then restore it from another machine. I sometimes use it to test data migrations because restoring a database dump takes a few seconds. 

I have been migrating from Docker to [OrbStack](https://orbstack.dev), and the only real pain point is moving data from one volume to another. I sometimes need to switch between the two, so I have recipes set to back up and restore my database from one context to another. 

```yml
# justfile

DATABASE_URL := env_var_or_default('DATABASE_URL', 'postgres://postgres@db/postgres')

# dump database to file
@pg_dump file='db.dump':
    docker compose run \
        --no-deps \
        --rm \
        db \
        pg_dump \
            --dbname "{{ DATABASE_URL }}" \
            --file /code/{{ file }} \
            --format=c \
            --verbose

# restore database dump from file
@pg_restore file='db.dump':
    docker compose run \
        --no-deps \
        --rm \
        db \
        pg_restore \
            --clean \
            --dbname "{{ DATABASE_URL }}" \
            --if-exists \
            --no-owner \
            --verbose \
            /code/{{ file }}
```

Shoutout to [Josh Thomas](https://social.joshthomas.dev/@josh) for help on this recipe since we both iterated on this for several projects.
