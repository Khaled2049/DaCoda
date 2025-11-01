---
date: "2025-11-01T09:03:00-06:00"
draft: true
title: How to Create a Blog
---

## Local Setup and Hugo Site Creation 

#### Prerequisites
1. Git installed.

2. Hugo installed - choco install hugo-extended --version=0.146.2 (on windows)

## Create the Site
Create a new Hugo site:

```Bash

hugo new site my-tech-blog
cd my-tech-blog
git init
```


### Add a Theme

Install the theme as a Git submodule (using PaperMod as an example):


Follow instructions from here: [Docs](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation)
```Bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

```Bash
hugo new content posts/my-first-project-post.md
```

## Configure the site
Open the main configuration file (config.yaml) and set your blog's details. The most important setting for deployment is the baseURL.

If you're using a User or Organization Page (repo named username.github.io), the URL is https://username.github.io/.

If you're using a Project Page (repo named something else, like my-tech-blog), the URL is usually https://username.github.io/my-tech-blog/.

Ini, TOML
```yml
baseURL = "https://khaled2049.github.io/DaCoder/"
languageCode = "en-us"
title = "My Technical Blog"
theme = "PaperMod"
```


```Bash

hugo server -D
Your site will be available at http://localhost:1313/. Press Ctrl + C to stop the server.
```