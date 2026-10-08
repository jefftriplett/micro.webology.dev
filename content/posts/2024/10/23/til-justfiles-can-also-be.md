---
title: "TIL Justfiles can also be Just Scripts "
date: "2024-10-23T12:04:47-05:00"
url: "/2024/10/23/til-justfiles-can-also-be/"
type: "post"
feed_id: "http://webology.micro.blog/2024/10/23/til-justfiles-can-also-be/"
categories: ["Justfiles", "Today I Learned"]
---

**Please note:** passing an argument like `--justfile` It only works on MacOS and on Linux. 

TIL that Justfiles can turn into Just Scripts by adding `#!/usr/bin/env just --justfile` to the top of the file and running `chmod +x` on the file.

From the docs:

> By adding a shebang line to the top of a `justfile` and making it executable, `just` can be used as an interpreter for scripts:
> https://github.com/casey/just?tab=readme-ov-file#just-scripts


## `just.sh`

```shell
#!/usr/bin/env just --justfile

@_default:
	just --justfile just.sh --list

@lint *ARGS:
    uv --quiet run --with pre-commit-uv pre-commit run {{ ARGS }} --all-files
```
After you run `chmod +x just.sh`, this file may be run using `./just.sh`, and sub-commands everything `just <subcommand>` will just work. 

Please note that `--justfile just.sh` is needed if you want your Just Script to be able to introspect or call itself. 

## Why? 

More and more of my clients are using Justfiles, and occasionally, I want some other recipes that may belong outside the default workflows. These can also be reusable between projects for some of my other internal tooling, so it's an excellent resource to learn about.
