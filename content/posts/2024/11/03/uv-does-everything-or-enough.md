---
title: "🤷 UV does everything or enough that I'm not sure what else it needs to do"
date: "2024-11-03T20:36:23-05:00"
url: "/2024/11/03/uv-does-everything-or-enough/"
type: "post"
feed_id: "http://webology.micro.blog/2024/11/03/uv-does-everything-or-enough/"
categories: ["Python", "UV", "Today I Learned"]
---

UV feels like one of those old infomercials where it solves everything, which is where we have landed in the Python world. 

I have had several discussions with friends about UV, and even when we talk about it during my weekly(ish) office hours, the list has grown to an ever-growing number of options. 

UV started as a quicker way of installing Python packages, and now it's easier to tell people that UV does everything and to focus on what it doesn't do.

My favorite feature is that UV can now bootstrap a project to run on a machine that does not previously have Python installed, along with installing any packages your application might require. 

Here is my incomplete list of what UV does today: 

- `uv pip install` replaces pip install
- `uv venv` replaces `python -m venv`
- `uv pip compile` replaces pip-tools compile
- `uv pip sync` replaces pip-tools sync
- `uv run` replaces pipx
- `uv tool run` replaces pipx
- `uv python` replaces pyenv, asdf, mise, and several other like-minded tools
- `uv build` - Build your Python package for pypi
- `uv publish` - Upload your Python package to pypi
- `astral-sh/setup-uv` brings UV to GitHub Actions
- `ghcr.io/astral-sh/uv:latest` brings UV and Python to Docker

I copied these four from `uv --help`, which feels like poetry features. 

- `uv add` - Add dependencies to the project
- `uv remove` - Remove dependencies from the project
- `uv sync` - Update the project's environment
- `uv lock` - Update the project's lockfile

## So what doesn't UV do?

UV does a lot, but it still needs to do everything. 

- UV doesn't run custom scripts defined in our `pyproject.toml` like [`npm-run-script`](https://docs.npmjs.com/cli/v10/commands/npm-run-script) allows. Thank you to [@command_tab](https://mastodon.social/@command_tab@hachyderm.io/113422203525133302) for jogging my memory. 
- UV doesn't convert my non-UV-based projects to UV. Converting is more about prefixing and replacing my commands to switch over. 
- UV doesn't manage, and bump version numbers like the [BumpVer](https://github.com/mbarkhau/bumpver), and others do.
- UV doesn't manage [pre-commit](/) like hooks. This is a long shot, but I'd love to see support via `pyproject.toml`. 
- UV doesn't replace Python, nor should it.
