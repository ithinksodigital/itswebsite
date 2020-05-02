---
layout: post
title: Building static website using HUGO
date: 2020-05-02T13:12:19.207Z
thumbnail: /images/uploads/hugo-logo-wide.svg
draft: false
tags:
  - news
---
Have you ever heard about Hugo? If not but you need to build your own website - portfolio, company page, product page or just a blog you definitely need to read this article. 

![Hugo logo ](/images/uploads/hugo-logo-wide.svg "Hugo logo")



> [Hugo](https://gohugo.io/) is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again. 

This is what you can read on Hugo's website. What is the most important it this tool? You don't need to have any special coding skills! Still interesting? Good! Let's start.

The easiest way to install Hugo on MacOS/ Linux is using Homebrew or Choco if you are using Windows.  To start just open your favoutire termial and type: 

```
brew install hugo
hugo version
```

Then Hugo will be installed. Command hugo version should return yout something like that like bellow, it mens that CLI was installed successfully. 

```
Hugo Static Site Generator v0.69.0/extended darwin/amd64 BuildDate: unknown
```

To create new page give the command: 

```bash
hugo new site blog
```

\
The above will create a new Hugo site in a folder named `blog`.