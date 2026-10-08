---
title: "⚙️ UV with GitHub Actions to run an RSS to README project"
date: "2024-10-05T12:43:54-05:00"
url: "/2024/10/05/uv-with-github-actions-to/"
type: "post"
feed_id: "http://webology.micro.blog/2024/10/05/uv-with-github-actions-to/"
categories: ["Django", "Python", "UV"]
---

For my personal [GitHub profile](https://github.com/jefftriplett/jefftriplett), I list my activities, affiliations, and the latest updates from some of my projects. 

Historically, I have used [JasonEtco/rss-to-readme](https://github.com/JasonEtco/rss-to-readme) GitHub Action to fetch a few RSS feeds or two and to update my README a few times a day. 

Overall, I'm happy with this setup. I used it on the Django News GitHub Organization to pull in newsletter issues, jobs, and the latest videos from our various projects. When I tried to install rss-to-readme in our repo, I was getting node12 errors. (Have I mentioned how much I loathe node/npm?). 

Instead of forking rss-to-readme and trying to figure out how to upgrade it, I used this as an excuse to "pair program" with [Claude](https://claude.ai). We quickly built out a prototype using Python and the [feedparser](https://github.com/kurtmckee/feedparser) library. 

I would share the chat log, but it's mostly me trying out a few different ways to invoke it before I settle on the finished approach. See the source code over on GitHub if you are curious: https://github.com/django-news/.github/blob/main/fetch-rss.py 

Once I had a working Python script that could fetch an RSS file and modify the README, I decided to run/deploy it using [UV](https://github.com/astral-sh/uv) to see how minimal I could build out the GitHub Action.
## GitHub Action

To run our `fetch-rss.py` script, we have four steps:

1. `actions/checkout` Get a git checkout of our project.
2. `astral-sh/setup-uv` Setup UV also installs Pythons for us. As a bonus, we enabled UV's cache support, which will run much faster in the future unless we change something in our fetch-rss.py file.
3. Run `uv run fetch-rss.py ...` to fetch our RSS feeds and write them to disk. `uv run` installs any dependencies and caches them before our `fetch-rss.py` runs.
4. `stefanzweifel/git-auto-commit-action` If our README.md file has changed, save our changes and commit them back to git and into our README.

Our `schedule.yml` GitHub Action workflow runs twice daily or whenever we push a new change to our repo. We also set `workflow_dispatch,` which gives us a button to run the script manually. 

```yaml
# .github/workflows/schedule.yml
name: Update README

on:
  push:
    branches:
      - main
  schedule:
    # Once a day at 12 AM
    - cron: 0 12 * * *
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest

    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v4

      - name: Install uv
        uses: astral-sh/setup-uv@v3
        with:
          enable-cache: true
          cache-dependency-glob: |
            *.py

      - name: Fetch our Feeds
        run: |
          # Fetch latest Django News Newsletter entries
          uv run fetch-rss.py \
              --section=news \
              --readme-path=profile/README.md \
              https://django-news.com/issues.rss

      - uses: stefanzweifel/git-auto-commit-action@v5
        with:
          commit_message: ":pencil: Updates README"
```
## Results

Overall, I'm pleased with this solution. If I wanted to spend more time on it or re-use this workflow, I might turn it into a GitHub Action workflow so that we can call: `django-news/rss-to-readme` to use in other projects. For now, this is fine. 

I'm happy with the `astral-sh/setup-uv` and `uv run` steps because they save me from having to set up Python and then install our project dependencies as separate steps. 

I normally shy away from running Python workflows like this in GitHub Actions because they involve a lot of slow steps. This entire workflow takes 16 to 20 seconds to run, which feels fast to me.
