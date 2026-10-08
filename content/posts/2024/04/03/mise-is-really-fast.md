---
title: "🚀 Mise is really fast"
date: "2024-04-03T19:27:03-05:00"
url: "/2024/04/03/mise-is-really-fast/"
type: "post"
feed_id: "http://webology.micro.blog/2024/04/03/mise-is-really-fast/"
categories: ["Python", "Today I Learned"]
aliases: ["/2024/04/03/mise-is-really.html"]
---

A month or two ago, I stumbled on [`justpath`](https://github.com/epogrebnyak/justpath), which is worth installing to help clean up any PATH environment issues you may or may not realize you have. 

I was frustrated because every time I created a new tab in iTerm2, it took three or more seconds for whatever slowed everything in my bash/dotfiles. 

With `justpath`, I found it straightforward to identify and address several paths related to ruby, rbenv, cargo, golang, and others that were causing issues. Rather than continue to fight these apps, I deleted them and removed them from my `.bash*` files. To see if I broke anything, I opened a new iTerm tab, and I had a new shell prompt in less than a second. 

Since I needed access to Ruby, NPM, and other tools, I  switched over to [`mise`](https://github.com/jdx/mise), which promises to be one tool for managing these languages and tools. `mise` is also written in Rust, so I know it's fast by default. 

To get started, check out Mise's [Quickstart](https://github.com/jdx/mise?tab=readme-ov-file#quickstart) docs in their README. I modified their bash example and added it to my `.bash*` files.

```shell
if command -v mise > /dev/null 2>&1; then
    eval "$(mise activate bash)";
fi
```

Once Mise was set up, and I opened a new tab, I installed Go, Node.js, Ruby, and Rust:

```shell
# to install Go
mise install golang

# to install Node.js
mise install node

# to install Ruby
mise install ruby

# to install Rust
mise install rust

# to reshim/add these tool to our path...
mise reshim
```

Eventually, I used Mise to install kubectl (boo) and yarn (hiss). Here is a list of everything on my older MacBook Pro that Mise is managing for me. 

```shell
$ mise list
Plugin   Version  Config Source    Requested
go       1.22.2
kubectl  1.22.2
node     20.10.0  ~/.tool-versions 20.10.0
ruby     3.3.0
rust     1.77.1
yarn     1.22.19
```

Another nice feature of Mise is that you can list the versions of each tool that you want Mise to install and manage for you in a `.tool-versions` file.

```shell
$ cat ~/.tool-versions
# direnv latest
# golang latest
# kubectl 1.22.2
# nodejs 18.9.1
# nodejs lts
# ruby 3.1.2
# starship latest
# yarn 1.22.19
nodejs 20.10.0
```

As a nice bonus, I discovered I could use Mise to manage the `direnv` and `starship` tools. In theory, Mise can also replace `direnv` with their built-in [environment](https://mise.jdx.dev/environments.html) support), but I haven't tried that feature yet. 

## Results

Mise is a nice win. I cut my new iTerm2 tab/session time down to close to 1/4 of a second, and I have more granular control over which exact versions of each tool I'm using. 

Overall, I still prefer to use [`pyenv`](https://github.com/pyenv/pyenv) to manage my Python versions, so I'm keeping that for now mainly because I use `pyenv-virtualenvwrapper` and a few other nice-to-haves. See my [Python Development on macOS Notes: pyenv and pyenv-virtualenvwrapper](/2024/02/10/python-development-on.html) article on why and how I manage those.
