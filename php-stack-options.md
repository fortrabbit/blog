---
created: 2025-09-24 19:05:04
author: fl
title: PHP + JS options
naviTitle: PHP + JS options
intro: Extending PHP by JS or not.
lead: Modern JavaScript enables interactive websites through live data exchange between browser and server. PHP excels at server-side processing, returning HTML or JSON responses. What options exist for combining PHP and JavaScript to create reactive websites?
wip: true
figure:
  emoji: 🧥
  color: rgba(222, 192, 103, 1)
head:
  meta:
    - name: 'keywords'
      content: 'JAMstack, react, vue, php, ajax, async, promise, stateful, fullstack'
---

This is a opinionated view from my angle of the web in 2025. It helps me thinking about the subject, since we want to cover a lot of this with our [new hosting platform](https://new.fortrabbit.com).

## What is a reactive websites anyway?

A website that uses JavaScript to update parts of the page (via XHR) by content coming from the server and by interaction of the user. This is my very own definition. Maybe it helps explaining what this is not:

- Not a static website, serving only full pages of HTML
- Not a classical serverful website, a server always renders a full page
- Not 'reactive web design', different website versions for each screen resolution

You may call it 'dynamic' but that is an equally empty shell. A Single Page Application (SPA) may the most prominent form of a reacyive website.

## Options

### No reactivity (classical page based)

Check your premises. Do you really need a reactive website? Classical server side rendered websites are way less complicated to build, maintain, deploy and host. Server side rendered pages come with great SEO options. Specifically for small website projects, with smaller teams or even solo developers. Don't follow the latest trends without consideration. For stateful elements or partial reactivity small drop-in JavaScript apps on a per page basis can work too.

This type does not require any complex interaction between frontend and backend and therefore is easy to deploy to a web host that supports PHP.

### Decoupled (headless)

- The PHP backend provides an API (REST, GraphQL).
- The frontend is based on JavaScript (Svelte, Next.js, Nuxt.js, Astro …)

See our [headless php post](/headless-php).

### Coupled (modern monoliths)

- The frontend part needs to be compiled during deployment.
- A Node.js runtime is required to serve the server side generated parts.

See our [modern PHP monoliths post](/modern-php-monoliths.md).

## My takeaway

This is not about winners and losers. This is about team size, requirements and most of it all personal preference and skills. Many developers stick to their home stack. My observation:

- Backend-focused devs try to get away without too much frontend.
- Frontend-focused devs try to get away without too much backend.

PHP has a bad reputation. And yes, the traditional approach where backend and frontend code are tightly coupled isn't sexy. But it's pragmatic!

For small and mid-sized website projects, I still would recommend to explore server-side rendered PHP. It's faster to develop, easier to deploy, and more affordable to host. In my humble opinion, the simplicity often outweighs the architectural superiority that decoupled systems provide.

The JAMstack evangelists promise a fast future on the edge. The technology is genuinely impressive, yet complex. More moving parts means higher hosting costs. Think twice, not every project justifies this investment.

It's also a matter of personal preference, many full stack developers enjoy working with JavaScript these days. In my eyes, the modern monolith is a path in the middle.
