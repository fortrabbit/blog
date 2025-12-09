# Blog

Welcome to the fortrabbit blog posts in markdown format.

## File structure

- `/images` optimized images that belong to the blog post

## Frontmatter syntax

```yml
title: Title as printed as H1 on the page
naviTitle: Optional shorter title
intro: This is a teaser text for the list view.
created: 2025-12-09 11:03:19
lead: This is larger text shown at the beginning of the article.
# Best use text + emoji or image
figure:
  text: Some text
  emoji: Some emoji
  icon: Name of Icones icon
  image: name of image file
  color: rgb(220,220,220)
  textColor: rgb(100,100,100)
# Best one tag
tags:
  - webdev
# Head is optional
head:
  meta:
    - name: 'keywords'
      content: 'fraud, spam, ai'
```

## How to create a blog post

1. Create a markdown file

## Working with DRAFTs

1. Start the file name with a `.my-blog-post.md` until it can get published

## Publishing the blog post

- Rename the file to `my-blog-post.md`
- Commit and push
- Then somehow it will be published next time frontend will be deployed
