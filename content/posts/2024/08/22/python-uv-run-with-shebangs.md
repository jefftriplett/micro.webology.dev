---
title: "🐍 Python UV run with shebangs"
date: "2024-08-22T13:54:45-05:00"
url: "/2024/08/22/python-uv-run-with-shebangs/"
type: "post"
feed_id: "http://webology.micro.blog/2024/08/22/python-uv-run-with-shebangs/"
categories: ["Python", "UV"]
---

This [UV shebang](https://simonwillison.net/2024/Aug/21/usrbinenv-uv-run/) trick that Simon Willison linked up is a nice pattern, and I plan to rebuild some of my one-off scripts in my [dotfiles](https://github.com/jefftriplett/dotfiles) using it. 

Here is a demo that will print "hello python" using the Python Branding colors using the [Rich](https://github.com/Textualize/rich) library while letting UV install and manage rich for you. 

```python
#!/usr/bin/env -S uv run
# /// script
# requires-python = ">=3.10"
# dependencies = [
#     "rich",
# ]
# ///

from rich.console import Console
from rich.theme import Theme

python_theme = Theme(
    {
        "pyyellow": "#ffde57",
        "pyblue": "#4584b6",
    }
)

console = Console(theme=python_theme)

console.print("[pyyellow]hello[/pyyellow] [pyblue]python[/pyblue]", style="on #646464")
```
Assuming you have UV installed, and you save and `chmod +x` this file as `hello-python.py`, then you should be able to run it via `./hello-python.py.`

I suspect I can more easily bootstrap new machines using this trick without fewer worries about polluting my global system packages.
