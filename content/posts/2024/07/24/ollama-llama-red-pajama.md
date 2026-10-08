---
title: "🦙 Ollama Llama 3.1 Red Pajama "
date: "2024-07-24T13:02:09-05:00"
url: "/2024/07/24/ollama-llama-red-pajama/"
type: "post"
feed_id: "http://webology.micro.blog/2024/07/24/ollama-llama-red-pajama/"
categories: ["Python", "Ollama", "LLM", "Today I Learned"]
aliases: ["/2024/07/24/ollama-llama-red.html"]
---

For a few weeks, I told friends I was excited to see if the new Llama 3.1 release was as good as it was being hyped. 

Yesterday, Llama 3.1 was released, and I was impressed that the [Ollama](https://ollama.com) project published a release to [Homebrew](https://brew.sh) and had the models ready to use. 

```shell
➜ brew install ollama

➜ ollama serve

# (optionally) I run Ollama as a background service
➜ brew services start ollama

# This takes a while (defaults to the llama3.1:8b model)
➜ ollama pull llama3.1:latest 

# (optional) This takes a longer time
➜ ollama pull llama3.1:70b

# (optional) This takes so long that I skipped it and ordered a CAT6 cable...
# ollama pull llama3.1:405b
```

To use chat with the model, you use the same `ollama` console command:

```shell
➜ ollama run llama3.1:latest
>>> how much is 2+2?
The answer to 2 + 2 is:
4!```

## Accessing Ollama Llama 3.1 with Python

The Ollama project has an [`ollama-python`](https://github.com/ollama/ollama-python) library, which I use to build applications. 

My demo has a bit of flare because there are a few options, like `--stream,` that improve the quality of life while waiting for Ollama to return results. 

```python
# hello-llama.py
import typer

from enum import Enum
from ollama import Client
from rich import print


class Host(str, Enum):
    local = "http://127.0.0.1:11434"
    the_office = "http://the-office:11434"


class ModelChoices(str, Enum):
    llama31 = "llama3.1:latest"
    llama31_70b = "llama3.1:70b"


def main(
    host: Host = Host.local,
    local: bool = False,
    model: ModelChoices = ModelChoices.llama31,
    stream: bool = False,
):
    if local:
        host = Host.local

    client = Client(host=host.value)

    response = client.chat(
        model=model.value,
        messages=[
            {
                "role": "user",
                "content": \
                    "Please riff on the 'Llama Llama Red Pajama' book but using AI terms like the 'Ollama' server and the 'Llama 3.1' model."
                    "Instead of using 'Llama Llama', please use 'Ollama Llama 3.1'.",
            }
        ],
        stream=stream,
    )

    if stream:
        for chunk in response:
            print(chunk["message"]["content"], end="", flush=True)
        print()

	else:
        print(f"[yellow]{response['message']['content']}[/yellow]")

if __name__ == "__main__":
    typer.run(main)
```

Some of my family's favorite books are the late Anna Dewdney's [Llama Llama books](https://llamallamabook.com). Please buy and support their work. I can't read Llama 3.1 and Ollama without considering the "Llama Llama Red Pajama" book.

To set up and run this:

```shell
# Install a few "nice to have" libraries
➜ pip install ollama rich typer

# Run our demo
➜ python hello-llama.py --stream

Here's a riff on "Llama Llama Red Pajama" but with an AI twist:

**Ollama Llama 3.1, Ollama Llama 3.1**
Mama said to Ollama Llama 3.1,
"Dinner's done, time for some learning fun!"
But Ollama Llama 3.1 didn't wanna play
With the data sets and algorithms all day.

He wanted to go out and get some rest,
And dream of neural nets that were truly blessed.
But Mama said, "No way, young Ollama Llama 3.1,
You need to train on some more NLP."

Ollama Llama 3.1 got so mad and blue
He shouted at the cloud, "I don't wanna do this too!"
But then he remembered all the things he could see,
On the Ollama server, where his models would be.

So he plugged in his GPU and gave a happy sigh
And trained on some texts, till the morning light shone high.
He learned about embeddings and wordplay too,
And how to chat with humans, that's what he wanted to do.

**The end**
```

## Connecting to Ollama

I have two Macs running Ollama and I use [Tailscale](https://tailscale.com) to bounce between them from anywhere. When I'm at home upstairs it's quicker to run a local instance. When I'm on my 2019 MacBook Pro it's faster to connect to the office. 

The only stumbling block I ran into was needing to set a few ENV variables setup so that Ollama is listening on a port that I can proxy to. This was frustrating to figure out, but I hope it saves you some time. 

```shell
➜ launchctl setenv OLLAMA_HOST 0.0.0.0:11434
➜ launchctl setenv OLLAMA_ORIGINS http://*

# Restart the Ollama server to pick up on the ENV vars
➜ brew services restart ollama
```

## Simon Willison's LLM tool

I also like using [Simon Willison](https://simonwillison.net)'s [LLM](https://llm.datasette.io/en/stable/) tool, which supports a ton of different AI services via third-party plugins. I like the [llm-ollama](https://pypi.org/project/llm-ollama/) library, which allows us to connect to our local Ollama instance. 

When working with Ollama, I start with the Ollama run command, but I have a few bash scripts that might talk to OpenAI or Claude 3.5, and it's nice to keep my brain in the same tooling space. LLM is useful for mixing and matching remote and local models. 

To install and use LLM + llm-ollama + Llama 3.1. 

Please note that the Ollama server should already be running as previously outlined. 

```shell
# Install llm
➜ brew install llm

# Install llm-ollama
➜ llm install llm-ollama

# List all of models from Ollama
➜ llm ollama list-models

# 
➜ llm -m llama3.1:latest "how much is 2+2?"
The answer to 2 + 2 is:

4
```

## Bonus: Mistral Large 2

While I was working on this post, Mistral AI launched their [Large Enough: Mistral Large 2](https://mistral.ai/news/mistral-large-2407/)  model today. The Ollama project released [support for the model](https://ollama.com/library/mistral-large) within minutes of its announcement. 

The Mistral Large 2 release is noteworthy because it outperforms Lllama 3.1's 405B parameter model and is under 1/3 of the size. It is also the second GPT-4 class model release in the last two days. 

Check out Simon's [post](https://simonwillison.net/2024/Jul/24/mistral-large-2/) for more details and another LLM plugin for another way to access it.
