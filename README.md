# Aum's blog

A blogging site made with [Hugo](https://gohugo.io/) using [papermod](https://themes.gohugo.io/themes/hugo-papermod/) theme. Contains all the technical stuff I have learned over the years, some of my projects and some of my thoughts.

## Basic setup 🔧
1. Install hugo
    - Debian based OS (PopOS, Ubuntu, Linux Mint)
        ```bash
        sudo apt install hugo
        ```
        However this may give an outdated version of Hugo so may not be compatable with some themes within the hugo themes community, installing with snap would likely give a newer version to install.
        ```bash
        sudo snap install hugo
        ```
    - RHEL and Fedora
        ```
        sudo dnf install hugo
        ```
    - Arch linux
        ```
        sudo pacman -S hugo
        ```

## Creating new files 📄
To create a new post, run the following command in the root directory of the project:
```bash
hugo new --kind post content/posts/<directory>/<filename>.md
```
Also check **Creating a new file - online > After the creation...(4)** for more details on how to change the file post creation.

## Working online 🌐
The project is designed to be worked online without any need for the volunteer/contributor to download the project or add any dependencies in the local environment. Just having a modern browser gives you the full ability to modifyh and edit the code.

**How does it work**💡
The application uses GitHub actions to do CI/CD in the web, this includes everything from creating new files with the preexisitng Hugo template, compiling everythingn in a github artifact and deploying into the web.

### Creating a new file - online 
![github actions list](https://raw.githubusercontent.com/AumPauskar/repo-media/8521e3544e2ec012bc35482ae009a64e1b2055cd/blog/hugo_github_actions.png)
- Open the GitHub actions tab in the actions tab and you'll see three options
- Use "Create New Hugo Post" option in the webpage.
- The action would ask about the file's root folder (within content/posts) and file's name (you have to add without the `.md` extension).
![creating a new post github actions](https://raw.githubusercontent.com/AumPauskar/repo-media/8521e3544e2ec012bc35482ae009a64e1b2055cd/blog/creating_new_file.png)
- After the creation of the new page ensure that you fill in the following details
    - `tags = [""]` will contain the tags which will help the user in searching for the required document. If multiple tags are required in the file then tags may be seperated by a comma `,` like the following `tags = ["python", "oops", "programming"]`
    - `author = ""` will contain your name. If multiple people are contributing to a file then the author's name may be seperated by a comma similar to the tags.
    - `description = ""` will contain a short description of the page. 

### Building the hugo site
The Hugo site is built automatically upon every push so the contributor doesn't need to manually trigger anything.

### Deploying the site
Click on the "Deploy Hugo site to Pages" and click run and the pages would run and deploy on the web ASAP. 
![meme](https://c.tenor.com/dxPl_UoR8J0AAAAC/tenor.gif)

## References
If you want to create a similar blog, you can follow the following links:
- [Hugo](https://gohugo.io/getting-started/quick-start/)
- [PaperMod theme](https://themes.gohugo.io/themes/hugo-papermod/)
- [Hugo in 100 seconds](https://youtu.be/0RKpf3rK57I?feature=shared)

## My links
- [Linktree](https://linktr.ee/aumpauskar)
- [Linkedin](https://www.linkedin.com/in/aum-pauskar-a5229b217/)
- [GitHub](https://github.com/AumPauskar)
- [Twitter/X](https://twitter.com/AumPauskar)