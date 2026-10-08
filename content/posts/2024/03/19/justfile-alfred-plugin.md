---
title: "Justfile Alfred Plugin"
date: "2024-03-19T12:49:25-05:00"
url: "/2024/03/19/justfile-alfred-plugin/"
type: "post"
feed_id: "http://webology.micro.blog/2024/03/19/justfile-alfred-plugin/"
categories: ["Python"]
aliases: ["/2024/03/19/justfile-alfred-plugin.html"]
---

A few years back, I had a productivity conversation with [Jay Miller](https://kjaymiller.com) about [Alfred](https://www.alfredapp.com) plugins, which led to him sharing his [Bunch_Alfred](https://github.com/kjaymiller/Bunch_Alfred) plugin. At the time, I played around with the [Bunch.app](https://bunchapp.co), a macOS automation tool, and Alfred's support was interesting. 

I created my Alfred plugin to run [Just](https://github.com/casey/just) command runner commands through my Alfred setup. However, I never got around to packing or writing the plugin's documentation. 

My Alfred plugin runs [Script Filter Input](https://www.alfredapp.com/help/workflows/inputs/script-filter/), which reads from a centrally located `justfile` and generates JSON output of all of the possible options. This will be displayed, and Alfred will run that command, whichever option you select. 

<img src="/uploads/2024/screenshot-2024-03-19-at-12.37.56-pm.png" width="600" height="403" alt="Alfred plugin showing a Just command with a list of recipe options to pick from.">

I was always unhappy with how the JSON document was generated from my commands, so I dusted off the project over lunch and re-engineered it by adding [Pydantic](https://github.com/pydantic/pydantic) support. 

Alfred just announced support for a new User Interface called [Text View](https://www.alfredapp.com/help/workflows/user-interface/text/), which could make text and markdown output from Python an exciting way to handle snippets and other productive use cases. I couldn't quite figure it out over lunch, but now I know it's possible, and I might figure out how to convert my Justfile Alfred plugin to generate better output. 


<script src="https://gist.github.com/jefftriplett/e7d4eade12e30001065eed2636010772.js"></script>
