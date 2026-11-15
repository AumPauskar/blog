+++
title = 'Automated Github to Gitlab Backup'
date = 2026-11-15T13:37:46Z
tags = ["ci/cd", "git", "github", "gitlab"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Just a reminder for me to remember how to backup repositories to gitlab incase github is inaccessible"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/blob/main/content"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Automated Github to Gitlab Backup

A paranoid guy always is ready for a doomsday scenario so let's prepare for a doomsday scenario. Backing up git from github to gitlab

## GitLab setup
1. Go to GitLab an an account is not created, create it
2. On the home page go to **Account icon > Preferences > Access > Personal access tokens** and you'll see a page like [this](https://gitlab.com/-/user_settings/personal_access_tokens?state=active&sort=expires_asc)

![GitLab PAT page](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/cloud/github-gitlab-backup/gitlab_pat_preview.png)

3. Create a legacy token

![Legacy token](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/cloud/github-gitlab-backup/gitlab_legacy_token.png)

4. It'll look something like this

![Legacy token page](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/cloud/github-gitlab-backup/generate_legacy_token.png)

5. Select only `read_repository` and `write_repository` here

![Legacy token scopes](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/cloud/github-gitlab-backup/legacy_token_scopes.png)

6. Now the Personal access tokens will be active throughout the repo

## GitHub setup
Unlike the Gitlab setup we're gonna go this in the scope of per repo. So only the repository you wanna backup gets backed up others stay the same

1. Go to any repo you wanna backup and go to **(Repo) Settings > Secrets and Variables > Actions > Repository secrets**
2. Create a **New repository secret** called as `GITLAB_TOKEN`

![GitHub settings](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/cloud/github-gitlab-backup/github_settings.png)

3. After the secret is active paste the following yaml script under `.github/workflows` and lets name this script `mirror-to-gitlab.yml`.
```yml
name: Mirror GitHub to GitLab

on:
  workflow_dispatch:

# Minimum permissions required
permissions:
  contents: read

# Prevent simultaneous mirror operations
concurrency:
  group: github-to-gitlab-mirror
  cancel-in-progress: false

jobs:
  mirror:
    name: Mirror main branch
    runs-on: ubuntu-latest

    # Only repository owner, and only when main is selected
    if: >
      github.actor == github.repository_owner &&
      github.ref == 'refs/heads/main'

    steps:
      - name: Clone GitHub main branch
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          GITHUB_REPOSITORY: ${{ github.repository }}
        run: |
          git clone \
            --single-branch \
            --branch main \
            "https://x-access-token:${GITHUB_TOKEN}@github.com/${GITHUB_REPOSITORY}.git" \
            source

      - name: Configure Git
        run: |
          git config --global user.name "GitHub Mirror"
          git config --global user.email "github-mirror@users.noreply.github.com"

      - name: Push main branch to GitLab
        env:
          GITLAB_TOKEN: ${{ secrets.GITLAB_TOKEN }}
        run: |
          git -C source push \
            --force \
            "https://oauth2:${GITLAB_TOKEN}@gitlab.com/<username>/<project/repo>" \
            main:main

      - name: Mirror result
        run: echo "Successfully mirrored GitHub main to GitLab main."
```
4. Modify **username** to **your own username** and **project/repo** to y**our own project/repo url**
5. The current workflow allows backup via a **manual workflow** dispatch and **only allows the repo owner in github to deploy** their own workflow so unauthorized user can't use it.