---
title: "🐚 My most used commands in my terminal history"
date: "2025-01-02T10:02:42-05:00"
url: "/2025/01/02/my-most-used-commands-in/"
type: "post"
feed_id: "http://webology.micro.blog/2025/01/02/my-most-used-commands-in/"
categories: ["Python"]
---

This post was inspired by [Andrea Grandi's](https://mastodon.social/@andreagrandi) [My ZSH history](https://www.andreagrandi.it/posts/my-zsh-history/) post, but I modified it back to work with my customized BASH output instead


```shell
➜ history | awk '{print $4}' | sort | uniq --count | sort --numeric-sort --reverse | head -10
11063 git
7636 just
3280 cd
2575 workon
1512 ls
1061 subl
 967 docker
 887 cat
 703 python
 700 gittower
```
I guess you could say I use `git` a lot. 


`just` is my main workflow driver. 


`workon` - I switched between projects 2575 times. 


`subl` and `gittower` are aliases to open [Sublime Text](https://www.sublimetext.com) and to open the existing project in [Git Tower](https://www.git-tower.com), respectively. 


I used `docker` more than I would have guessed, but `just` tends to wrap most of that workflow, or it would have given `git` a run for its money.
