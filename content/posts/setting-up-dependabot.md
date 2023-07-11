---
title: "Setting Up GitHub Dependabot for New Project"
date: 2023-07-10T22:35:21-04:00
draft: false
tags: ["GitHub", "Dependabot", "Repo", "Tutorial"]
---

We're always on the lookout for ways to make project management smoother and more efficient. Today, we'll be exploring how to set up GitHub Dependabot for a new project. Dependabot is a fantastic tool from GitHub that can help you maintain your project's dependencies, by automatically opening pull requests to update them.

# Step 1: Create Your .github Folder

Kickstart by creating a `.github` folder right at the root directory of your repository. This folder will house GitHub-specific files, including our Dependabot configuration file.

# Step 2: Add Your Dependabot Configuration

Next, inside the `.github` folder, you need to create a file named `dependabot.yml`. This YAML file will contain the configuration settings for Dependabot. Here's a template to start off with:

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"
    automerge: true
    reviewers:
      - "username1"
      - "username2"
    labels:
      - "dependencies"
      - "automerge"
    ignore:
      - dependency-name: "react"
        versions: ["16.x.x"]
```

Let's briefly discuss each of these settings:

- `package-ecosystem` specifies the package manager. For a Node.js project, use "npm".
- `directory` indicates where your package files are stored. For most projects, this will simply be the root directory ("/").
- `schedule.interval` sets how often Dependabot will check for updates. In this example, it checks daily.
- `automerge` allows Dependabot to automatically merge updates that pass your CI tests.
- `reviewers` lists GitHub usernames to automatically assign for reviewing version updates.
- `labels` will automatically apply the listed labels to the Dependabot's PRs.
- `ignore` lets you specify certain dependencies that you do not wish Dependabot to update.

Be sure to fill out the relevant sections according to your project's needs.

# Step 3: Push Your Changes to Git

After setting up your `dependabot.yml` file, it's time to push the changes to Git. You can do this using the usual git add, git commit, and git push commands.

# Step 4: Voilà, You're Done!

And just like that, you've set up GitHub Dependabot for your new project! This fantastic bot will now help you in maintaining your project's dependencies.