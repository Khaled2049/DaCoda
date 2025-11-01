---
date: "2025-11-01T09:03:00-06:00"
draft: false
title: How to Create a Blog Using HUGO and Github Pages
---

## Local Setup and Hugo Site Creation 

#### Prerequisites
1. Git installed.

2. Hugo installed - choco install hugo-extended --version=0.146.2 (on windows). Follow steps from the docs for other OS

## Create the Site
Create a new Hugo site:

```Bash

hugo new site my-tech-blog
cd my-tech-blog
git init
```


### Add a Theme

Install the theme as a Git submodule (using PaperMod as an example). You'll find other settings to custimze the blog inside the repos config.yaml


Follow instructions from here: [Docs](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation)
```Bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

## To create content
```Bash
hugo new content posts/my-first-project-post.md
```
Remember to change draft to True to see the Blog.

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

# Set up Github pages
This next section will outline the steps needed to setup github actions to deploy the website. 

### Configure GitHub Pages Deployment
We will deploy from a branch that GitHub Pages can serve (usually gh-pages). No need to create it manually gitHub Actions will handle that. In your repo, create the directory: `.github/workflows/` Then add a file named deploy.yml

```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches:
      - main  # deploy whenever you push to main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          submodules: true  # fetch theme if it's a git submodule
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build site
        run: hugo --minify

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

### In github
Go to your repository on GitHub → Settings → Pages
Under Source, choose:
Deploy from a branch
Branch: gh-pages
Folder: / (root)

### Enable GitHub Actions write permissions

Go to your repository → Settings → Actions → General
Scroll to Workflow permissions
Select: [x] Read and write permissions

### Create a .gitignore
```
/public/
/resources/
```

Push changes to github and view your website. 



