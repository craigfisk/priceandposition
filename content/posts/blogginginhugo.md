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
description: "Blogging in markdown in the PaperMod them on the Hugo framework is simple, fast, and perfect for the web (and used here)."
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

{{< figure src="/image/justin-lim-tloFnD-7EpI-unsplash.jpg" caption="Blogging in markdown in the PaperMod theme on the Hugo framework is simple, fast, and perfect for the web (and used here)" >}}

Why?

Three reasons to use Hugo:

1. The writing is about as **simple** as it gets. You use [markup](https://en.wikipedia.org/wiki/Markdown) (called _markdown_, naturally) designed for simplicity and web output. What is _markup_? It's like writing \*\*bold\*\* to get **bold**. Check out a [cheatsheet](https://www.markdownguide.org/cheat-sheet/) to get an idea.
2. Edits result in almost **instant** changes locally, which can be **automatic** on your website, too, if hosting your blog on services like Netlify, Github pages, or Digital Ocean (details below). It's fast, because it runs on Hugo, a very fast framework on the very fast Go (golang) programming language, used in many cloud and web infrastructure applications.
3. Finally, how could anything named for **[Victor Hugo](https://en.wikipedia.org/wiki/Victor_Hugo)** not be great? (["Les misérables](https://en.wikipedia.org/wiki/Les_Mis%C3%A9rables)," ["The Hunchback of Notre-Dame"](https://en.wikipedia.org/wiki/The_Hunchback_of_Notre-Dame), and so much more.)

## Installation (and assumptions)

If not running the base software (or it's out-of-date), go to https://go.dev and https://gohugo.io to **install** or **update**. To check what is running:

```bash
    go --version
    hugo --version
```

**Assumptions**: you have experience using _git_, working with repos, and have accounts on Github and Netlify (could also be Github pages or Digital Ocean, but I don't cover those).

Create a **project directory** using Hugo and add the _PaperMod_ theme as a _submodule_. This enables _PaperMod_ to stay up-to-date **independent** of your repo.

```bash
   hugo new my_blog
   cd my_blog
   git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
   git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

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

Anytime you want to change _anything_, you do that by creating a **replacement file** in your directory structure with the same name and content as the corresponding original file in the PaperMod theme subdirectory, and then you change (add, subtract) the part you want to be different. For example,

TBD:

- TOC _shortcode_ added to \_index.md ??
- Images to in static/image.
