---
title: "🐘 Docker Postgres Autoupgrades"
date: "2024-06-29T23:54:41-05:00"
url: "/2024/06/29/docker-postgres-autoupgrades/"
type: "post"
feed_id: "http://webology.micro.blog/2024/06/29/docker-postgres-autoupgrades/"
categories: ["Docker", "Postgres"]
aliases: ["/2024/06/29/docker-postgres-autoupgrades.html"]
---

Upgrading Postgres in Docker environments can be daunting, but keeping your database up-to-date is essential for performance, security, and access to new features. While there are numerous guides on manually upgrading Postgres, the process can often be complex and error-prone. Fortunately, the [pgautoupgrade](https://hub.docker.com/r/pgautoupgrade/pgautoupgrade) Docker image simplifies this process, automating the upgrade dance for us.

## The Challenge of Upgrading Postgres

For many developers, upgrading Postgres involves several manual steps: backing up data, migrating schemas, ensuring compatibility, and testing thoroughly. Mistakes during these steps can lead to downtime or data loss, making the upgrade process a nerve-wracking experience.

The `pgautoupgrade` Docker image is designed to handle the upgrade process seamlessly. Using it in place of the base Postgres image allows you to automate the upgrade steps, reducing the risk of errors and saving valuable time.
## How to Use pgautoupgrade

While you can use the `pgautoupgrade` directly with Docker, I prefer it as my default development image. 

I set my `compose.yml` config with `pgautoupgrade` similar to this config: 

```yml
# compose.yml
services:
  db:
    image: "pgautoupgrade/pgautoupgrade:latest"
    volumes:
      - postgres_data:/var/lib/postgresql/data/
# ...
```

Instead of using the latest version of Postgres, `pgautoupgrade` can be set to a specific version. This is nice if you want to match whichever version of Postgres you use in production or if you have extensions that might not be ready to move. 

```yml
# compose.yml
services:
  db:
    image: "pgautoupgrade/pgautoupgrade:16-alpine"
    volumes:
      - postgres_data:/var/lib/postgresql/data/
# ...
```

Overall, I'm happy with `pgautoupgrade`. Please note that using `pgautoupgrade` does not mean you should not make data backups. 

See my last article, [🐘 A Just recipe to back and restore a Postgres database](/2024/06/28/a-just-recipe.html) to learn some tips on how to automate using `pg_dump` and `pg_restore`.
