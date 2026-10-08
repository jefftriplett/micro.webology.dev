---
title: "🧱 Django ModelForm Template starting point"
date: "2024-06-08T23:56:56-05:00"
url: "/2024/06/08/django-modelform-template-starting-point/"
type: "post"
feed_id: "http://webology.micro.blog/2024/06/08/django-modelform-template-starting-point/"
categories: ["Django", "Python", "Today I Learned"]
---

Recently, I have been doing a lot of Django formwork. I start with a basic template like `form.as_div` or `form|crispy` until it grows uncomfortable.

Today, I was bouncing between two projects, and I noticed I was working on the tasks that had grown uncomfortable to the point that I dreaded working on the templates. 

While I enjoy working with Django's template system, I was putting off these tasks, and all they had in common was finishing some of the form and template work. 

I couldn't quite understand why this was such a mental blocker, so I stopped working, disconnected, and mowed my yard. Thankfully, that did the trick. 

As I finished mowing, I realized that I was struggling to complete these tasks because I was overwhelmed by needing to dump all the form fields into a template. 

Once I realized why I was feeling this resistance, I realized I needed to focus on solving this issue to move on. 

I remembered Daniel Roy Greenfeld's [Rapidly creating smoke tests for Django views](https://daniel.feldroy.com/posts/2024-05-rapidly-creating-smoke-tests-for-django-views) from a few weeks ago, where he made a management command to print out a bunch of smoke tests. 

I decided to try the same technique by passing a string path to a Django ModelForm and printing out my form template. 

**Edit:** [micro.blog](https://micro.blog) did not like the templates in templates from my Python script, so I had to swap out the inline example with a gist. Sorry about that. 

<script src="https://gist.github.com/jefftriplett/3ca8bb4a4b97bdecec3a257ff5cd1cf9.js"></script>

This template could be better, but it was good enough. I tested it on a few of the forms I'm using on [Django News Jobs](https://jobs.django-news.com), and it's an improvement over what I started with. 

Something was in the water because when I checked our company Slack, Frank Wiles showed me his new [make-management-command](https://github.com/frankwiles/make-management-command) project, which takes a similar approach to creating the folders and files needed to create a new management command.
