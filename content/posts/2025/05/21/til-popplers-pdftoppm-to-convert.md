---
title: "TIL Poppler's pdftoppm to convert PDF pages into PNG files"
date: "2025-05-21T12:26:57-05:00"
url: "/2025/05/21/til-popplers-pdftoppm-to-convert/"
type: "post"
feed_id: "http://webology.micro.blog/2025/05/21/til-popplers-pdftoppm-to-convert/"
categories: ["Today I Learned"]
---

Today I learned about [`pdftoppm`](https://www.xpdfreader.com/pdftoppm-man.html), a simple CLI tool that can convert each page of a PDF into separate image files. 

My use case was to chop up a few big PDF reports to make OCR and data analysis easier, but scanning them a page at a time. 
## Install

I'm using [Homebrew](https://brew.sh) on macOS, but Poppler will also run on Linux and other operating systems.

```shell
$ brew install poppler
```
## Quick Usage

```shell
$ pdftoppm -png -rx 300 -ry 300 input.pdf output
```
- `-png` -> save the output files as PNG images
- `-rx 300 -ry 300` -> set the output resolution to 300 dpi
- `input.pdf` -> your source file which you want to process
- `output` -> Your output file prefix which will produce `output-1.png`, `output-2.png`, ...
