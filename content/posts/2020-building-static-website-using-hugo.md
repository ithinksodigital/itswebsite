---
layout: post
title: Building static website using HUGO
date: 2020-05-02T13:12:19.207Z
thumbnail: /images/uploads/hugo-cli-img-social.png
draft: false
tags:
  - hugo webdevelopment staticwebsite website
---
Have you ever heard about Hugo? If not but you need to build your own website - portfolio, company page, product page or just a blog you definitely need to read this article. 

![Hugo logo ](/images/uploads/hugo-logo-wide.svg "Hugo logo")



> [Hugo](https://gohugo.io/) is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again. 

This is what you can read on Hugo's website. What is the most important it this tool? You don't need to have any special coding skills! Still interesting? Good! Let's start.

The easiest way to install Hugo on MacOS/ Linux is using Homebrew or Choco if you are using Windows.  To start just open your favourite terminal and call: 



```bash
brew install hugo
hugo version
```

Then Hugo will be installed. Command `hugo version`  should return your something like bellow, it means that CLI was installed successfully. 



```bash
Hugo Static Site Generator v0.69.0/extended darwin/amd64 BuildDate: unknown
```

To create new site give the command: 

```bash
hugo new site blog
```

\
The above will create a new Hugo site in a folder named `blog`. Change directory to this path and run local server which is built in inside Hugo.  Server will be automatically run on port 1313 so if you open your browser and visit http://localhost:1313/ your page will be display. Now page is blank because there is no content there. You have to add theme. 

```bash
hugo server -D
```

\
To do it the easiest way is [visit Hugo website](https://themes.gohugo.io/) where you can find a lot of ready to use themes. Some of them are suit for product page, portfolio or blog for which I need. I've chosen theme named [hugo-theme-slim](https://github.com/zhe/hugo-theme-slim). When you choose one which you want to use just visit the themes Github repository and clone it to your website directory. 

![git hub clone](/images/uploads/clone-git.gif)



```bash
cd themes
git clone https://github.com/zhe/hugo-theme-slim slim
```

The last thing which you have to do is add theme to your site. To do it just edit the config.toml in root folder of your project. How this file will be looking depends on which theme you chosen. In general for sure you have to add a line indicating which theme will be use by Hugo. But better find in your theme folder **exampleSite** directory and copy all content form config.toml your own. 

At this moment you can also change the baseURL to your domain address. 

```bash
baseURL = "http://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = 'slim'

[params]
  Subtitle = "Your site's subtitle/tagline"
  GithubID = "Your Github ID"
  TwitterID = "Your Twitter ID"
  AnalyticsID = "Your Google Analytics tracking code"
  DisqusShortname = "Your Disqus shortname"
  Summary = true  # takes true or false
  Content = false  # takes true or false
  # if both are set to true, summary is shown.
  # FooterMsg = "Copyright Me 2016. Powered by Hugo."
  mainSections = ["post"]
```

Quite easy, right? Ok, but it was supposed to be a blog! Yes, adding the new blog post is also so easy. Look on your config file there should be something like: 

```
mainSections = \["post"]
```

It means that all your post have to be in post folder. Ok so create new folder named **post** under the content directory. To add new blog post just create new file like title-my-blog-post.md or what you prefered. But very important is to keep the *.md extensions. Hugo to rendering new conted is using Markdown language. It is saved in plain text format but includes inline text symbols that define how to format the text. Markdown language has very simple syntax which you want to check [here](https://guides.github.com/features/mastering-markdown/). 

![](/images/uploads/dir-tree.png)

Sample blog post bellow:

```markdown
+++
title = "Blog post"
date = 2020-04-21T21:36:10+02:00
draft = false
+++
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Etiam pharetra cursus turpis, laoreet venenatis diam varius eu. 
Maecenas feugiat, est ac auctor scelerisque, dui eros ornare quam, vel vestibulum neque sapien et sapien. Cras congue, augue eu tristique ullamcorper, justo dui euismod dolor, quis faucibus eros turpis id mauris. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec dolor magna, imperdiet et lacinia id, suscipit vel velit. Aliquam luctus leo sit amet magna tempor, in aliquet dolor placerat. Donec eget aliquet purus. Donec feugiat dapibus ipsum et iaculis. Cras convallis nec elit ut porta. Vestibulum dignissim auctor tincidunt. Duis hendrerit, nibh sit amet tempor porttitor, diam felis vulputate mauris, ut tincidunt mauris nisi at magna.


```

The part between plus signs is something like setting of your entries. Bellow the settings real content of your post. Now if you save this file new post will be added to your home page Thats all.

If you don't want to publish you post immediately just change draft from false to true. 

Build static pages[](https://gohugo.io/getting-started/quick-start/#step-7-build-static-pages)? Just call:

```
hugo -D
```

Output will be in`/public/`directory. All what is inside this directory just copy to your sever and voilà your site is online.



![](/images/uploads/screenshot-2020-05-02-at-21.25.11.png)