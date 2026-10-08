---
title: "🤖 I released files-to-claude-xml and new development workflows"
date: "2024-10-12T14:00:31-05:00"
url: "/2024/10/12/i-released-filestoclaudexml-and-new/"
type: "post"
feed_id: "http://webology.micro.blog/2024/10/12/i-released-filestoclaudexml-and-new/"
categories: ["Django", "Python", "LLM"]
---

After months of using and sharing this tool via a private gist, I finally carved out some time to release [files-to-claude-xml](https://github.com/jefftriplett/files-to-claude-xml). 


Despite my social media timeline declaring LLMs dead earlier today, I have used [Claude Projects](https://www.anthropic.com/news/projects) and Artifacts. 


My workflow is to copy a few files into a Claude Project and then create a new chat thread where Claude will help me write tests or build out a few features. 


My `files-to-claude-xml` script grew out of some research I did where I stumbled on their [Essential tips for long context prompts](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/long-context-tips#essential-tips-for-long-context-prompts) which documents how to get around some file upload limits which encourages uploading one big file using Claude's XML-like format. 


With `files-to-claude-xml`, I build a list of files that I want to import into a Claude Project. Then, I run it to generate a `_claude.xml` file, which I drag into Claude. I create a new conversation thread per feature, then copy the finished artifacts out of Claude once my feature or thread is complete. 


After the feature is complete, I delete the `_claude.xml` file from my project and replace it with an updated copy after I re-run `files-to-claude-xml`. 


## Features on the go


One bonus of using Claude Projects is that once everything is uploaded, I can use the Claude iOS app as a sort-of notes app and development tool. I can start parallel conversation threads and have it work on new ideas and features. Once I get back to my desktop, I can pull these chat conversations up, and if I like the direction of the feature, I might use them. If not, I have wasted no time or effort on them. This also serves as a nice ToDo list. 


## New workflows 


I am working on side projects further using this methodology. Sometimes, I would like to work on something casually while watching Netflix, but my brain shuts off from coding during the day. Instead of feeling bad that I haven't added share links to a website or some feature I meant to add last week, I can pair Claude to work on it with me. 


I can also get more done with my lunch hours on projects like [DjangoTV](https://djangotv.com) than I could have otherwise. Overall, I'm happy to have an on-demand assistant to pair with and work on new features and ideas. 


It's also quicker to try out new ideas and projects that I would have needed to make time for. 


## Alternatives


Simon Willison wrote [files-to-prompt](https://github.com/simonw/files-to-prompt), which I think is also worth trying. I contributed to the discussion, feedback, and document structure for the `--cxml` feature. 


I wrote `files-to-claude-xml` before Simon had cxml support and hoped to not release my version. 


However, after trying it out on several projects, my ignore/exclude list grew more significant than the files that I wanted to include in my project to send to Claude. I found it easier to generate a list of files to pass to mine instead of maintaining a long list to exclude.
