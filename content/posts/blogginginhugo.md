---
title: Blogging with Victor Hugo
date: 2022-01-21T18:29:07-06:00
# weight: 1
# aliases: ["/first"]
tags: ["blog", "blogging", "Hugo", "golang", "PaperMod"]
author: "Craig Fisk"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Blogging in PaperMod on Hugo is simple, fast, and up-to-date (and used here)."
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

<!-- {{< figure src="/image/justin-lim-tloFnD-7EpI-unsplash.jpg" caption="Blogging in PaperMod on the Hugo framework, named for 19th-century French author Victor Hugo, is simple, fast, and perfect for the web (and used here)" >}} -->

{{< figure src="/image/Cosette-sweeping-les-miserables-emile-bayard-1862_400.jpg" caption="Cosette in 'Les Misérables' by French author Victor Hugo, namesake of the Hugo framework. Hugo is simple, fast, and up-to-date (and used here)" >}}

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

**Assumptions**: you have experience using _git_, working with repos, and have accounts on Github and Netlify (or Github pages or Digital Ocean, but I don't cover those). Also, the examples assume Linux (or Linux environments like [Darwin](<https://en.wikipedia.org/wiki/Darwin_(operating_system)>) on the Mac, or Windows Subsystem for Linux [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) or [git bash](https://www.stanleyulili.com/git/how-to-install-git-bash-on-windows/) on Windows).

Create a **project directory** using Hugo and add the **_PaperMod_** theme as a **_submodule_**. This enables _PaperMod_ to stay up-to-date **independent** of your repo.

```bash
   hugo new site <name of site> -f yml
   // PaperMod theme uses .yml instead of .toml to write config files
   cd my_blog
   git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
   git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

## Configuration

If you really want to save time, **copy** the styling and layout of [https://priceandposition.com](https://priceandposition.com). You can adapt the configuration file below (_config.yml_ instead of .toml, see on installation above). Everything should be pretty self-evident.

PaperMod can do a lot not included here in the interest of simplicity. For a complete description, see the writeup by Aditya Telange, the author of _PaperMod_: ["Installation"](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/).

````bash
baseURL: "https://priceandposition.com"
languageCode: en-us
title: "Price and Position"
draft: false  # If true, publishes on git push; if false, "hugo server -D" to see it.
theme: "PaperMod"
paginate: 10 # was 5 by default
...

params:
  env: production # Needed to enable google analytics, opengraph, twitter-cards, etc.
  title: Price and Position
  description: "Business and tech"
  keywords: [Blog, Portfolio, PaperMod]
  author: Craig Fisk   # if multiple authors, use a list of strings:
  ...

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


It's configured. Let's run it locally:

```bash
    hugo server -D      // Includes any posts marked "draft: true".
    localhost:1313      // Your site; ctrl-click to open in browser.

````

The goal here is just to provide a basic **mental model** for how to work with PaperMod and Hugo, and to set up automatic updates on Netlify, so that a push to Github updates the site.

## Changes

To change _anything_, create a **replacement file** in **your directory tree** with the same name and content as the corresponding original file in the **PaperMod theme subdirectory tree**, and then change (or add, or subtract) the part to modify.

Here are the **relevant parts**, showing the output from [_tree_](https://www.geeksforgeeks.org/tree-command-unixlinux/).

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

## Adding features

Want to add a feature? Here are some ways.

**1)** Using **shortcodes**, which are pre-defined for elements such as Figure (photo with caption), YouTube, or TOC (Table of Contents). A shortcode is a small template to add some function. ["Use Hugo's Built-in Shortcodes"](https://gohugo.io/content-management/shortcodes/#use-hugos-built-in-shortcodes). Or ["Create Your Own Shortcodes"](https://gohugo.io/templates/shortcode-templates/).

**2)** Using **partials** to define what goes into an element, such as a footer or header.

**3)** Using **archetypes**, which have their own directory and define the "master" version of something. For example, **archetypes/post.md** defines what goes into a new blog post by default.

Examples:

- To add a [TOC (Table of Contents)](https://gohugo.io/content-management/toc/) to the homepage in https://priceandposition created by PaperMod and my configuration

```bash
  layouts/partials/home_info.html
```

```html
{{- with $.Site.Params.homeInfoParams }}
<article class="first-entry home-info">
  <header class="entry-header">
    <h1>{{ .Title | markdownify }}</h1>
  </header>
  <section class="entry-content">
    <p>{{ .Content | markdownify }}</p>
  </section>
  <section class="entry-content">
    <p>{{ .TableOfContents }}</p>
  </section>
  <footer class="entry-footer">
    {{ partial "social_icons.html" $.Site.Params.socialIcons }}
  </footer>
</article>
{{- end -}}
```

The TOC _shortcode_ (in double squiggle brackets) has been inserted in a new section as

```html
<section class="entry-content">
  <p>{{ .TableOfContents }}</p>
</section>
```

- To add images (like .jpg or .png files of photos from [Unsplash](https://unsplash.com/) and [Pexels](https://www.pexels.com/)), put them in static/image, and reference them in an HTML5-like _figure_. This can have attributes like a caption, title, alt, width, etc.

- [Disqus](https://disqus.com/) (comments) or [cactus.chat](https://cactus.chat/) and [Drift](https://drift.om) (bots > "conversational marketing")

- [Wowchemy widgets](https://wowchemy.com/)

- In the homepage icons, I created and added a Marmalade icon to link to my startup at [https://marmalade.ai](https://marmalade.ai). You could do something similar.

## Netlify

Assuming you have Github and Netlify accounts, you want to set it up with your site hosted on Netlify so that anytime you push to Github your site automatically updates:

**1)** **Login to Netlify** and "Add a New Project." If you already have a project (the case here), click to go to it. You'll see "Site settings" and "Domain settings".

**2)** Click **"Domain Settings"**. When finished, it will look like:

{{< figure src="/image/Screenshot at 2022-01-23 15-38-35.png" caption="*Custom Domains* when complete will look like this for your domain name." >}}

You **prove ownership** of the domain by accessing your account on your provider to have the domain's **nameservers point to Netlify**. Go to your domain registrar ([Namecheap](https://www.namecheap.com/), [GoDaddy](https://www.godaddy.com/), [Google Domains](https://domains.google.com/)), then to the domain you are using (acquire it first, obviously, if necessary), and set its **nameservers** to **point to Netlify**.

For "priceandposition.com" on Namecheap, that looks like

{{< figure src="/image/Screenshot at 2022-01-23 16-00-57.png" caption="Don't forget to click the green *checkmark* at top right when finished to save!" >}}

Wait. Might take **24-48 hours** for the result to flow through to Netlify. There's a button at the bottom to check whether Netlify has seen confirmation (the effect of the nameserver change on your domain host) that you own the domain. You will then have

```bash
  priceandposition.netlify.com
```

and can edit the other two listings to refer to your **actual domain.**

```bash
  priceandposition.com
```

By the way, there's no need to worry about a **[Letsencrypt](https://letsencrypt.com)** certificate. Getting **https** is part of the deal. Netlify takes care of that. So you can use [https://priceandposition.com](https://priceandposition.com).

While you are waiting for confirmation (might be quick; might be overnight), you may want to read Victor Hugo's "Les misérables" - [translation](https://www.gutenberg.org/files/135/135-h/135-h.htm)]/[original](https://www.gutenberg.org/files/17489/17489-h/17489-h.htm).

**3)** Link to your Github account.

To get to the next step, hit the "back" button and then the _Site overview_ button, as shown in the menu below:
{{< figure src="/image/Screenshot at 2022-01-23 18-13-57.png" caption="Click tne *back* button and then the *Site overview* button on the top level menu and then *Build & deploy*." >}}

Click link to _Site overview_ > _Build & deploy_.

**4)** Build settings.

From the "Site overview" menu, click "Build & deploy." Notice that at the top right it says

```bash
  Settings for Continuous Deployment from a Git repository
```

Yay! That's what we want.

There are several things to **configure** on this page.

a) First off, at the top as shown here, set your **repo url** on Github.

{{< figure src="/image/Screenshot at 2022-01-23 18-32-47.png" caption="Set your *repository*, *build command*, and *publish directory*." >}}

b) The _build command_ should be **hugo** and the _publish directory_ should be **public**.

c) Below, in the _Branches_ section, you probably want to set it to **main** and to deploy only the production branch.

d) Further down, under _Environment Variable_ set key/value pairs as

```bash
    HUGO_ENV      production
    HUGO_VERSION  0.91.2  // whatever "hugo --version" returns on localhost
```

**5)** Try it out from your development system!

```bash
    hugo        // build the site
    git add .   // assuming you are already running a git project
    git commit -m 'Update for deployment'
    git push [origin main]
    // In maybe 10 seconds, the website on Netlify is updated
```

You'll still see typos and things to improve, but updates are so much **faster and effortless**. The _hugo_ commands are so fast it seems like nothing happened.
