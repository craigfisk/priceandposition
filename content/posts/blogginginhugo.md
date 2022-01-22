---
title: Blogging In Hugo
date: 2022-01-21T18:29:07-06:00
# weight: 1
# aliases: ["/first"]
tags: ["blog", "blogging", "Hugo", "golang", "PaperMod"]
author: "Craig Fisk"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: true
hidemeta: false
comments: false
description: "Blogging in PaperMod on Hugo is simple, fast, and perfect for the web (and used here)."
canonicalURL: "https://priceandposition.com/content/"
disableHLJS: true # to disable highlightjs
disableShare: true
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "Making snakes is really easy in modelling clay." # alt text
    caption: "Making snakes is really easy in modelling clay." # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

<!-- Photo by <a href="https://unsplash.com/@justinlim?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Justin Lim</a> on <a href="https://unsplash.com/s/photos/cartoon-of-caveman?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a> -->

{{< figure src="/image/justin-lim-tloFnD-7EpI-unsplash.jpg" caption="Blogging in PaperMod on the Hugo framework is simple, fast, and perfect for the web (and used here)" >}}

Why?

Three reasons to use PaperMod and Hugo:

1. It makes producing a blog about as **simple** as it gets. You use [markup](https://en.wikipedia.org/wiki/Markdown) (called _markdown_, naturally) designed for simplicity and web output. What is _markup_? It's like writing \*\*bold\*\* to get **bold**. Check out a [cheatsheet](https://www.markdownguide.org/cheat-sheet/) to get an idea.
2. Edits result in almost **instant** changes locally, which can be **automatic** on your website, too, if hosting your blog on services like **Netlify** (like the current site), Github pages, or Digital Ocean (details below). It's fast, because it runs on Hugo, a very fast framework on the very fast Go (golang) programming language, used in many cloud and web infrastructure applications.
3. Finally, how could anything named for **[Victor Hugo](https://en.wikipedia.org/wiki/Victor_Hugo)** not be great? (["Les misérables](https://en.wikipedia.org/wiki/Les_Mis%C3%A9rables)," ["The Hunchback of Notre-Dame"](https://en.wikipedia.org/wiki/The_Hunchback_of_Notre-Dame), _c'est formidable!_)

## Installation (and assumptions)

If not running the base software (or it's out-of-date), go to https://go.dev and https://gohugo.io to **install** or **update**. To confirm what is running:

```bash
    go --version
    hugo --version
```

**Assumptions**: you have experience using _git_, working with repos, and have accounts on Github and Netlify (could also be Github pages or Digital Ocean, but I don't cover those). Also, the examples assume Linux (or [Darwin](<https://en.wikipedia.org/wiki/Darwin_(operating_system)>) on Mac, [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) or [git bash](https://www.stanleyulili.com/git/how-to-install-git-bash-on-windows/) on Windows).

Create a **project directory** using Hugo and add the **_PaperMod_** theme as a **_submodule_**. This enables _PaperMod_ to stay up-to-date **independent** of your repo.

```bash
   hugo new site <name of site> -f yml
   // PaperMod theme uses .yml instead of .toml to write config files
   cd my_blog
   git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
   git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

## Configuration

If you really want to save time, **duplicate** the styling and layout of [https://priceandposition.com](https://priceandposition.com). Just copy and modify as appropriate, the configuration file below (_config.yml_ instead of .toml, see on installation above). Everything should be pretty self-evident. For a complete description, see writeup by Aditya Telange, the author of _PaperMod_: ["Installation"](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/).

```bash
baseURL: "https://priceandposition.com"
languageCode: en-us
title: "Price and Position"
draft: false  # If true, publishes on git push; if false, "hugo server -D" to see it.
theme: "PaperMod"
paginate: 10 # was 5 by default
enableRobotsTXT: true
buildDrafts: false
buildFuture: false
buildExpired: false
# googleAnalytics: UA-123-45

minify:
  disableXML: true
  minifyOutput: true

params:
  env: production # Needed to enable google analytics, opengraph, twitter-cards, etc.
  title: Price and Position
  description: "Business and tech"
  keywords: [Blog, Portfolio, PaperMod]
  author: Craig Fisk   # if multiple authors, use a list of strings:
  images: ["<link or path of image for opengraph, twitter-cards>"]
  DateFormat: "January 2, 2006"
  defaultTheme: auto #creates the "night mode"/"day mode" switch at top.
  disableThemeToggle: false
  ShowReadingTime: true
  ShowShareButtons: true
  ShowPostNavLinks: true
  ShowBreadCrumbs: true
  ...

  homeInfoParams:
    Title: "Business and tech"
    Content: Blog of [Craig Fisk](https://linkedin.com/in/craigfisk), Minneapolis-St. Paul

  socialIcons:
    - name: "marmalade"
      url: "https://marmalade.ai"
    - name: linkedin
      url: "https://linkedin.com/in/craigfisk"
    - name: github
      url: "https://github.com/craigfisk"
    - name: twitter
      url: "https://twitter.com/craigfisk"
  ...
menu:
  main:
    - identifier: home
      name: home
      url: /
      weight: 5
    - identifier: posts
      name: blog
      url: /posts/
      weight: 7
      ...
    - identifier: tags
      name: tags
      url: /tags/
      weight: 20
      ...
```

## Mental Model, part 1:

To change _anything_, create a **replacement file** in **your directory** structure with the same name and content as the corresponding original file in the **PaperMod theme subdirectory**, and then change (or add, or subtract) the part to modify. For example,

Here are the **relevant parts** of the resulting structure in [_tree_](https://www.geeksforgeeks.org/tree-command-unixlinux/)

```bash
   tree -d  // just the directories

   .
├── archetypes  // Footers, headers, what does the default post look like, etc.
├── content
│   ├── posts   // Your posts land here, created by "hugo new posts/my_post.md"
...
├── layouts     // Any of your own changes to theme layouts go here.
│   └── partials
...
├── static
...
│   └── image   // Any images you are using. Access in blog code as "image/my_image"
└── themes
    └── PaperMod
    ...
        └── layouts
            ├── _default
            │   └── _markup
            ├── partials
            │   └── templates
    ...

```

## Mental Model, part 1:

How do you add some specific features? There are three ways. Using pre-defined **shortcodes**, as in the TOC (Table of Contents) example below. A shortcode is a small template to implement a particular functionality using your data or environment. You can ["Use Hugo's Built-in Shortcodes"(https://gohugo.io/content-management/shortcodes/#use-hugos-built-in-shortcodes) You can also ["Create Your Own Shortcodes"](https://gohugo.io/templates/shortcode-templates/). Examples of built-in shortcodes:

### Photo with caption

```markdown
    {{< figure src="/image/my_photo.jpg" caption="This is the caption for my photo" >}}
    // Relative to the root of the project, this is /static/image/my_photo.jpg
```

### YouTube video embedded

````markdown
    {{< youtube id="w7Ft2ymGmfc" title="A New Hugo Site in Under Two Minutes" >}}
    <!-- "w7Ft2ymGmfc" links to the video: https://www.youtube.com/watch?v=w7Ft2ymGmfc, "A New Hugo Site in Under Two Minutes"

```

TBD:

- TOC _shortcode_ added to \_index.md ??
- Images to in static/image.
- Hugo uses the [Blackfriday](https://github.com/russross/blackfriday) flavor of markdown.
```
````
