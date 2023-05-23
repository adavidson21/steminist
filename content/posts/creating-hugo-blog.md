---
title: "Creating a Website Using Hugo and Github Pages"
date: 2023-05-21T19:09:51-04:00
lastmodified: 2023-05-21T19:09:51-04:00
draft: false
tags: ["Hugo", "GitHub", "webdev"]
---

Welcome, **STEMinist** readers! Today, we'll dive into crafting a website with Hugo (a cool static site generator) and hosting it on GitHub Pages. Let's get started!

### 1. Install `Hugo` on your computer. 

First off, you need to install Hugo on your machine. For PC users, Chocolatey is your best friend, and for macOS, Homebrew has got your back.   
```bash
// For PC
choco install hugo-extended

// For macOS
brew install hugo
``` 

If you haven't been introduced to Chocolatey or Homebrew yet, check out the [alternative installation methods for Hugo](https://gohugo.io/installation/).  

### 2. Pick a Hugo Theme

Hugo has an impressive library of templates. Take a peek, grab something that vibes with you, and snag the code from GitHub as a zip file. For instance, I'm rocking the [LoveIt](https://github.com/dillonzq/LoveIt) template for this blog.

### 3.Set Up Your GitHub Repository

Time to create a public GitHub repository for your site. From there, go to 'Settings' > 'Pages'. Enable Pages and under 'Build and Deployment', select 'GitHub Actions' in the source dropdown.

### 4. Tidy Up Your Repository

Add a .gitignore file with the following entries: 

```txt 
    public/
    /exampleSite/resources/
    /exampleSite/.hugo_build.lock
    node_modules/
    build/
```

Next up, we're creating a `.github` folder with a `workflows` subfolder. Inside `workflows`, we'll need a `hugo.yaml` file.


### 5. Set Up GitHub Pages Workflow

Alright, we'll populate `hugo.yaml` with the following code (as found in [Hugo's guide to deployment](https://gohugo.io/hosting-and-deployment/hosting-on-github/)), which will get your GitHub Pages workflow in gear:
   
```yaml
  # Sample workflow for building and deploying a Hugo site to GitHub Pages
  name: Deploy Hugo site to Pages

  on:
    # Runs on pushes targeting the default branch
    push:
      branches:
        - main

    # Allows you to run this workflow manually from the Actions tab
    workflow_dispatch:

  # Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
  permissions:
    contents: read
    pages: write
    id-token: write

  # Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
  # However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
  concurrency:
    group: "pages"
    cancel-in-progress: false

  # Default to bash
  defaults:
    run:
      shell: bash

  jobs:
    # Build job
    build:
      runs-on: ubuntu-latest
      env:
        HUGO_VERSION: 0.111.3
      steps:
        - name: Install Hugo CLI
          run: |
            wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
            && sudo dpkg -i ${{ runner.temp }}/hugo.deb
        - name: Install Dart Sass Embedded
          run: sudo snap install dart-sass-embedded
        - name: Checkout
          uses: actions/checkout@v3
          with:
            submodules: recursive
            fetch-depth: 0
        - name: Setup Pages
          id: pages
          uses: actions/configure-pages@v3
        - name: Install Node.js dependencies
          run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
        - name: Build with Hugo
          env:
            # For maximum backward compatibility with Hugo modules
            HUGO_ENVIRONMENT: production
            HUGO_ENV: production
          run: |
            hugo \
              --gc \
              --minify \
              --baseURL "${{ steps.pages.outputs.base_url }}/"
        - name: Upload artifact
          uses: actions/upload-pages-artifact@v1
          with:
            path: ./public

    # Deployment job
    deploy:
      environment:
        name: github-pages
        url: ${{ steps.deployment.outputs.page_url }}
      runs-on: ubuntu-latest
      needs: build
      steps:
        - name: Deploy to GitHub Pages
          id: deployment
          uses: actions/deploy-pages@v2
```

### 6. Bring In the Hugo Template

Unzip your downloaded Hugo template code into the root folder of your GitHub repository. Your folder structure should look something like this:

```
├── .github
│   ├── workflows
│   │   ├── hugo.yaml
│   ├── css
│   │   ├── **/*.css
│   ├── images
│   ├── js
│   ├── index.html
├── .gitignore 
├── content
├── resources
├── themes
│   ├── [Theme Name]
└── config.toml 
```

Keep in mind that folders like `content`, `resources`, `themes`, and files like `config.toml` may vary based on the theme you've chosen.

### 7. Personalize Your Theme

Now, tweak your theme as per its specific documentation. Run hugo serve from your project's root (where `config.toml` resides) to preview your site locally.

### 8. Commit and Push Changes

Happy with your tweaks? Commit and push 'em to your GitHub repository. Pro tip: run `hugo serve` before pushing changes to make sure everything's copacetic.

### 9. Verify Deployment

Head over to "Actions" in your GitHub repository. Under "All Workflows", find the run corresponding to your latest commit. Once complete, its indicator should turn green.

### 10. Take a Peek at Your Live Website

Click on your latest commit message. Under "deploy", you'll find the link to your newly-minted website. Go ahead and check it out!

And there it is! You've just built and deployed a website using Hugo and GitHub Pages. Your site will update automatically with each new change that's pushed. Enjoy your new digital presence and happy coding!