---
title: Hello Teutonic CSS
created: 2018-08-02
published: true
author: fl
excerpt: Some details on our open source CSS framework.
lead: So we said to do more open source on fortrabbit. TADA – here is my first big open source publication. A CSS framework.
keywords: SCSS, CSS, CSS custom properties
image: teutonic-poster.jpg
tag:
  - webdev
---


**TLDR; Check it our yourself: [teutonic.co](https://teutonic.co)**

## Why yet another CSS framework?

I am the design guy here. My aim is to make fortrabbit look unique. In order to do so, I have developed the "fortrabbit.css" which is currently in use on the page you are reading. For future fortrabbit projects it needed further generalization and I also wanted some fancy new extras.

First off,  I needed use cases - think of HTML markup to develop the framework against. Those examples became a kind of documentation and specification. They even live in their own repo. It's like test-driven development for CSS. From there it was only a small step to open source it. Check out this [Medium post](https://medium.com/@frank_laemmer/yet-another-css-framework-6f5a9b142b43), if your more interested in my motivations behind it.

## Who is it for?

Sophisticated web designers who care about design details.

## What's so special about it?

It makes use of CSS vars (CSS custom properties), which enables great theming options. You can work with compiled CSS directly. It has multiple ways to display content grids, see my [Medium post](https://medium.com/@frank_laemmer/using-flexbox-and-css-grid-together-71b7f6e219a5) on why I am using Flexbox and CSS grid together. It uses modular scale for spacing and typography. It has unique form styles. And much more.

## How can I use it?

You can just hotlink the CSS file and adjust it using CSS vars to your needs, this actually works quite well. Or you can get the source code and integrate in your own build process. The source is in SCSS — without any extras — so most systems can run the build out of the box.

## Why doesn't it use any PHP?

Doesn't have to. It has less dependencies and is more open. The documentation is Jekyll and it get's build on GitHub pages.

## What's next?

Teutonic CSS looks familiar to the styles you can see on these pages currently, just more versatile and clean. Teutonic CSS will be the groundwork for upcoming fortrabbit projects. It will also be further developed with that. I have quite a few ideas on how to enhance it. For now, I am happy about feedback and issues you might have.

## Where is it again?

Hop over to: **[teutonic.co](https://teutonic.co)**
