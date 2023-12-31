+++
title = 'Static site generators with Hugo'
date = 2023-11-17T09:19:25+05:30
draft = false
+++

# Static site generators
A short guide on how this site was created using hugo.

## Introduction
There are multiple ways of creating of a website, if for example a simple site needs to be created with minimal content and updates a **static site** might be adequate, however if the site needs a frontend, backend and a database then a **dynamic site** is required. If the content is the only thing that matters and the content needs to be updated regularly then a static site generator is required. Multiple static site generators are avalable as open source projects, one of them is **jeckyll** from github and the other is **hugo** that is optimized for minmal loadtime.

**Note:** This documentation is written for linux (debian) based systems, for windows, WSL can be installed to run it.

## Installation
To install hugo first open a **linux shell** and then type the following commands.
```bash
sudo apt update
sudo apt install hugo -y
```

However for the use of the latest version in Debian based operating systems using snap is **reccommended**. **INSTALLATION OF THE APT VERSION MAY CAUSE PROBLEMS**
```bash
sudo snap install hugo
```

Typing `hugo version` will give a confirmation that the software has been installed sucessfully. Checking for the **hugo extended version** is reccommended.

```
hugo v0.120.4-f11bca5fec2ebb3a02727fb2a5cfb08da96fd9df+extended linux/amd64 BuildDate=2023-11-08T11:18:07Z VendorInfo=snap:0.120.4
```
If the version of hugo then building the software from source is reccommended. 

Hugo can also be installed in a native Windows OS using chocolatey using this command. However this will require a git terminal to run.
```bash
choco install hugo -confirm
```


After the installation of hugo is complete, the version can be checked by typing the following command.
```bash
hugo version
```

## Creating a new site
To create a new site, first create a new folder and then navigate to that folder using the terminal. Then type the following command to create a new site.
```bash
hugo new site <site-name>
```

## Adding content to the new site
Content can be added in the new site by the use of this command

```bash
hugo new content posts/optional subfolders/.../filename.md
```

```bash
hugo new content posts/my-first-post.md
```
Filename of `my-first-post.md` can be replaced with other filenames also but the extension of the filename must end with a `.md` for singnifying the markdown syntax. Another way of adding content is directly adding the file in the `content` folder, however this is not reccommended, since it will not reflect in the archetypes folder and the file templates will not be generated.


This might be the contents of the file
```
+++
title = 'My First Post'
date = 2023-11-15T23:52:11+05:30
draft = true
+++
## Introduction

This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!
```
**Make sure the draft section is changed from true to false**

## Setting up a theme
There are a lot of themes available on hugo to chech the themes visit the [hugo themes site](https://themes.gohugo.io/). Most of the themes have a github clone link available, it may start via this `git submodule add <github link>`. All the theme files are stored in the themes folder and the most important thing is to remember the official name of your theme. For example if your theme name is `ananke` then that themename must be configured in `hugo.toml`.

### Setting up `hugo.toml`
If you are using the latest version of hugo then there should be a file called `hugo.toml`. There are 2 crutial changes in it. \
Example
```toml
baseURL = 'https://yourdesireddomain.top-level-domain-name/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ananke'
```
First one is changing `baseURL` where the custom domain name and adding a new line of `theme` and adding the **corresponding theme name**. These two are the crutial changes, however you can also change the website title by using the `title` tag and the rendered language by `languageCode`.

## Creating and viewing in a draft server

To run the site in the local server this command can be used.
```bash
hugo server -D
```

or this can be used
```bash
hugo server --buildDrafts
```
These two commands will display all the contnents of the site, including the drafts site (note that there was the section `drafts = true` in the markdown file). To check whether the file is marked as drafts or not and to check if it's render in the production site can be done by this command

```bash
hugo server
```

## Generating the site
All the content generated till now is just the drafts and will not render in the actual site. To generate the site the following command can be used. Go to the site's root directory and type the following command.

```bash
hugo
```

This will generate the site in the `public` folder. To view the site in the local server the following command can be used.

```bash
hugo server
```

## Deploying the site
The best way to deploy the site is to use a free service like Firebase, Netlify or Github pages. To deploy the site in github pages the following steps can be followed.

1. Create a new repository in github with the name `<username>.github.io`
2. Push the whole site to the repository. (Assuming git is installed and `git init` has been run in the root directory of the site.)
	```bash
	git add -A
	git commit -m "Initial commit"
	git remote add origin <your_github_link>
	git branch -M main
	git push -u origin main
	```
3. Go to the repository settings and scroll down to the `Github Pages` section and change the source to **Github Actions (beta)**. 
4. Create a file at this location `.github/workflows/hugo.yaml`.
5. Copy the following code in the file. **Change the hugo version to the local hugo version on your machine**.
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
		HUGO_VERSION: 0.120.2
		steps:
		- name: Install Hugo CLI
			run: |
			wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
			&& sudo dpkg -i ${{ runner.temp }}/hugo.deb          
		- name: Install Dart Sass
			run: sudo snap install dart-sass
		- name: Checkout
			uses: actions/checkout@v4
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
			uses: actions/upload-pages-artifact@v2
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

6. Commit the changes and push it to the repository.
	```bash
	git add -A
	git commit -m "Added github actions"
	git push
	```
7. Check the deployments section in the repository to check if the deployment is sucessful or not.
8. If the deployment is sucessful then the site should be available at `https://<username>.github.io`

## Finishing touches
To make the site more reachable and to make it more SEO friendly, the following steps can be followed.
- Register the site in [google search console](https://search.google.com/search-console/)
- Register the site in [google analytics](https://analytics.google.com/)

- Few more notes
	- `robots.txt` and `sitemap.xml` are automatically generated by hugo and can be found in the `public` folder.
## References
- [Hugo quickstart](https://gohugo.io/getting-started/quick-start/)
- [Hugo themes](https://themes.gohugo.io/)
- [Hugo deployment](https://gohugo.io/hosting-and-deployment/hosting-on-github/)