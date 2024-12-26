+++
date = '2024-12-22T14:19:12-08:00'
draft = false
title = 'Hugo - static site generator'
toc = true
## Hugo will create http://localhost:1313/tags/web-dev/
tags = ['web dev']
+++
Hugo is one of the most popular open-source static site generators. With its amazing speed and flexibility, Hugo makes building websites fun again.

And this is how this web site was built.
<!--more-->

## Learning

1. [Learning resources](https://gohugo.io/getting-started/external-learning-resources/)
2. [Hugo documentation](https://gohugo.io/documentation/)
3. [Hugo documentation hugo.toml](https://github.com/gohugoio/hugoDocs/blob/master/hugo.toml)

## Installation and setup

### Install Hugo

1. Install Hugo for Debian Linux (ChromeOS) `sudo dpkg -i /mnt/chromeos/MyFiles/Downloads/hugo_extended_0.140.1_linux-amd64.deb` binaries are from [hugo/releases](https://github.com/gohugoio/hugo/releases)
2. Unfortunately Debian package repo has very old version, but `sudo apt install hugo` still works.

### Site creation and configuration

1. Create new site `hugo new site belablotski`
2. Install theme `git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke` and add `theme = 'ananke'` in [hugo.md](./hugo.md)
3. [Commenting systems](https://gohugo.io/content-management/comments/)
4. [Syntax highlighting](https://gohugo.io/content-management/syntax-highlighting/)
5. [Links and cross references](https://gohugo.io/content-management/cross-references/)

### Hosting

1. [GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

### Code

1. [Directory structure](https://gohugo.io/getting-started/directory-structure/)

## Content creation

### Pages

1. Create page `hugo new content content/posts/my-first-post.md`
2. Page bundles and [_index.md](https://gohugo.io/content-management/organization/#index-pages-_indexmd)

### Context organization

1. [Taxonomies](https://gohugo.io/content-management/taxonomies/). Taxonomy, term, value.
2. [Default taxonomimes](https://gohugo.io/content-management/taxonomies/#default-taxonomies). Hugo automatically creates taxonomies for `tags` and `categories` (unless `disableKinds` turns it off).
3. [Configure taxonomies](https://gohugo.io/content-management/taxonomies/#configure-taxonomies)
4. [Assign terms to content](https://gohugo.io/content-management/taxonomies/#assign-terms-to-content): `categories = ['Category A', 'Category B'] tags = ['Tag A', 'Tag B']`. [Taxonomic weight](https://gohugo.io/content-management/taxonomies/#order-taxonomies) - ordering.

|Kind|Description|Example|
|----|-----------|-------|
|home|The landing page for the home page|/index.html|
|page|The landing page for a given page|my-post page (/posts/my-post/index.html)|
|section|The landing page of a given section|posts section (/posts/index.html)|
|taxonomy|The landing page for a taxonomy|tags taxonomy (/tags/index.html)|
|term|The landing page for one taxonomy’s term|term awesome in tags taxonomy (/tags/awesome/index.html)|

### Templates

1. [Page kings](https://gohugo.io/content-management/taxonomies/#default-taxonomies): home, page (=single), section, taxonomy, and term. Single `layouts/_default/single.html`, list page (section listings, home page, taxonomy lists, taxonomy terms) `layouts/_default/list.html`
2. [Template types](https://gohugo.io/templates/types/) ([base](https://gohugo.io/templates/types/#base), [home](https://gohugo.io/templates/types/#base), [single](https://gohugo.io/templates/types/#single), [section](https://gohugo.io/templates/types/#section), [taxonomy](https://gohugo.io/templates/types/#taxonomy)) and [Lookup order](https://gohugo.io/templates/lookup-order/)
3. `type` (page type) - this is a sub-folder in `layouts` folder, `layout` is a sub-folder under `layouts/page_type`.


## Preview and publish

### Preview

1. Local site `hugo server`
2. Preview your work before publishing `hugo server --buildDrafts --buildFuture`
3. `hugo server --navigateToChanged`