---
title: "📓 My notes on publishing a Python package with UV and building a custom GitHub Action for files-to-claude-xml "
date: "2024-10-16T23:07:08-05:00"
url: "/2024/10/16/my-notes-on-publishing-a/"
type: "post"
feed_id: "http://webology.micro.blog/2024/10/16/my-notes-on-publishing-a/"
categories: ["Python", "Docker", "UV", "Today I Learned"]
---


My new Python application [files-to-claude-xml](https://pypi.org/project/files-to-claude-xml/) is now on PyPI, which means they are packaged and pip installable. My preferred way of running `files-to-claude-xml` is via UV's tool run, which will install it if it still needs to be installed and then execute it.


```shell
$ uv tool run files-to-claude-xml --version
```

## Publishing on PyPi with UV


UV has both build and publish commands, so I took them for a spin today. 


`uv build` just worked, and a Python package was built.


When I tried `uv publish`, it prompted me for some auth settings for which I had to log in to [PyPI](https://pypi.org) to create a token. 


I added those to my local ENV variables I manage with [direnv](https://direnv.net). 


```shell
export UV_PUBLISH_PASSWORD=<your-PyPI-token-here>
export UV_PUBLISH_USERNAME=__token__
```

Once both were set and registered, `uv publish` published my files on PyPI. 


## GitHub Action


To make `files-to-claude-xml` easier to run on GitHub, I created a custom action to build a `_claude.xml` from the GitHub repository. 


To use this action, I wrote this example workflow, which runs from [files-to-claude-xml-example](https://github.com/jefftriplett/files-to-claude-xml-example)


```yaml
name: Convert Files to Claude XML


on:
  push


jobs:
  convert-to-xml:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Convert files to Claude XML
      uses: jefftriplett/files-to-claude-xml-action@main
      with:
        files: |
          README.md
          main.py
        output: '_claude.xml'
        verbose: 'true'
    - name: Upload XML artifact
      uses: actions/upload-artifact@v4
      with:
        name: claude-xml
        path: _claude.xml
```

My GitHub action is built with a `Dockerfile`, which installs `files-to-claude-xml`.


```Dockerfile
# Dockerfile
FROM ghcr.io/astral-sh/uv:bookworm-slim


ENV UV_LINK_MODE=copy


RUN --mount=type=cache,target=/root/.cache/uv \
    --mount=type=bind,source=uv.lock,target=uv.lock \
    --mount=type=bind,source=pyproject.toml,target=pyproject.toml \
    uv sync --frozen --no-install-project


WORKDIR /app


ENTRYPOINT ["uvx", "files-to-claude-xml"]
```

To turn a GitHub repository into a runnable GitHub Action, an `action.yml` file needs to exist in the repository. This file describes the input arguments and which `Dockerfile` or command to run. 


```yml
# action.yml
name: 'Files to Claude XML'
description: 'Convert files to XML format for Claude'
inputs:
  files:
    description: 'Input files to process'
    required: true
    type: list
  output:
    description: 'Output XML file path'
    required: false
    default: '_claude.xml'
  verbose:
    description: 'Enable verbose output'
    required: false
    default: 'false'
  version:
    description: 'Display the version number'
    required: false
    default: 'false'
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - ${{ join(inputs.files, ' ') }}
    - --output
    - ${{ inputs.output }}
    - ${{ inputs.verbose == 'true' && '--verbose' || '' }}
    - ${{ inputs.version == 'true' && '--version' || '' }}
```

Overall, this works. Claude's prompting helped me figure it out, which felt fairly satisfying given the goal of `files-to-claude-xml`.
