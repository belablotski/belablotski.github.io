# Learning

1. [Learning resources](https://gohugo.io/getting-started/external-learning-resources/)
2. [Hugo documentation](https://gohugo.io/documentation/)
3. [Hugo documentation hugo.toml](https://github.com/gohugoio/hugoDocs/blob/master/hugo.toml)

# Installation and setup

## Install Hugo

1. Install Hugo for Debian Linux (ChromeOS) `sudo dpkg -i /mnt/chromeos/MyFiles/Downloads/hugo_extended_0.140.1_linux-amd64.deb` binaries are from [hugo/releases](https://github.com/gohugoio/hugo/releases)
2. Unfortunately Debian package repo has very old version, but `sudo apt install hugo` still works.

## Site creation and configuration

1. Create new site `hugo new site belablotski`
2. Install theme `git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke` and add `theme = 'ananke'` in [hugo.md](./hugo.md)
3. [Commenting systems](https://gohugo.io/content-management/comments/)
4. [Syntax highlighting](https://gohugo.io/content-management/syntax-highlighting/)
5. [Links and cross references](https://gohugo.io/content-management/cross-references/)

## Hosting

1. [GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

## Code

1. [Directory structure](https://gohugo.io/getting-started/directory-structure/)

# Pages

1. Create page `hugo new content content/posts/my-first-post.md`
2. [_index.md](https://gohugo.io/content-management/organization/#index-pages-_indexmd)

# Preview and publish

## Preview

1. Local site `hugo server`
2. Preview your work before publishing `hugo server --buildDrafts --buildFuture`
3. `hugo server --navigateToChanged`