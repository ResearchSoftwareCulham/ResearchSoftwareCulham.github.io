# Contributing
We welcome contributions from people working on research software around Culham.

This guide summarises the [Github guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll) for adding new content to a Jekyll site. The "publishing source" is the `master` branch; anything added to `master` will be published automatically. Firstly, please create an issue and branch for the content you wish to add.

There are two main types of content, pages and posts, both written in Markdown. A page is permanent, without an associated date, whereas a post has a date associated with it.

## Adding a blog post
In the `_posts` directory, create a new Markdown file of the form `YYYY-MM-DD-NAME-OF-POST.md` (it's easiest to copy and edit the `_posts/2021-03-15-welcome-to-jekyll.md` file). Then add the YAML front matter:
```yaml
---
layout: post
title: "POST TITLE"
date: YYYY-MM-DD hh:mm:ss -0000
categories: CATEGORY-1 CATEGORY-2
---
```

Below this, add the Markdown content for your post.

## Adding a page
In the project root directory, create a new file in the form `PAGE-NAME.md` (or copy and edit the `about.md` file). Then add the YAML front matter:
```yaml
---
layout: page
title: "PAGE TITLE"
permalink: /URL-PATH/
---
```

Below this, add the Markdown content for your post.

## Previewing changes
Once you've set up Jekyll locally (see the `README.md`), you can preview your changes using:
```
bundle exec jekyll serve
```

and navigating to http://localhost:4000.

## Publishing
Open a pull request for the changes on your branch. Once merged to `master`, the content will be published on [researchsoftwareculham.github.io](https://researchsoftwareculham.github.io/), which is public.