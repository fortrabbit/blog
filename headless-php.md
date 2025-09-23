---
created: 2025-09-22 20:14:44
author: fl
title: Headless PHP
naviTitle: Headless PHP
intro: Decoupled websites with PHP and JS.
lead: Decopuled systems. Frontend in JavaScript. Backend in PHP. Why. How. If.
wip: true
figure:
  emoji: 🧥
  color: rgba(222, 192, 103, 1)
  textColor: rgba(129, 95, 71, 1)
  text: Where is my mind?
head:
  meta:
    - name: 'keywords'
      content: 'JAMstack, react, vue, php, ajax, async, promise, stateful, fullstack'
---

## What is headless?

A software system where the front end (user interface) is separated from the back end (content management). It's called headless, because the backend content system is now missing the part where it renders the frontend.

This decoupled dual stack approach consists of two independent systems that talk to each other.

- The backend provides an API (REST, GraphQL).
- The frontend is based on JavaScript (Svelte, Next.js, Nuxt.js, Astro …)

### PHP as the backend

The backend of a JAMstack can be anything. From a Firebase database, to a hosted CMS like Contentful. We provide PHP hosting. So let's look at that.

#### CMS systems

Traditional PHP CMS systems bundle the backend and the frontend into one system. But a headless mode is now available for WordPress, Craft CMS and many more.

- [getkirby.com/…/headless-getting-started](https://getkirby.com/docs/cookbook/headless/headless-getting-started)
- [craftcms.com/…/graphql.html](https://craftcms.com/docs/getting-started-tutorial/more/graphql.html)
- [statamic.dev/rest-api](https://statamic.dev/rest-api)

#### PHP frameworks

PHP frameworks like Laravel and Symfony support API interfaces as well. The PHP backend system and the frontend system can live in separate codebases and can be developed and deployed independently. This makes it interesting for bigger teams or projects as well as frontend focused developers. The frontend website is just one client for the backend, another one might be a mobile app.

The use of Single Page Applications is a trend. Carefully consider if such a system is the best technology for the given project. For decoupled projects, the individual parts can be deployed to different web hosts:

- PHP backend: a service that has a PHP runtime.
- JS frontend: a dedicated JAMstack hosting service.

This is sophisticated, more complex and more expensive to host. It's also important to choose the correct delivery mode that comes with strings attached in regard of hosting:

### Client Side Rendered (CSR)

This is the classical Single Page App (SPA) style. All the data is provided by the API to the frontend via AJAX calls. The website is constructed in the browser when a human visits.

#### CSR hosting

Best use CSR (classical SPA) for app-like projects, not websites. Something that has a login and does do not require any SEO. The frontend and the backend can be indipendently deployed and hosted. The frontend is cheap to host, since it's just some text files. It can also be put on the edge.

### Server Side Generated (SSG)

During build time, usually during deployment, the whole frontend content is pre-rendered as static HTML pages. The initial load will display the static page (fast), then the SPA mode can serve every click from them then on.

#### SSG hosting

SSG works great for small sites with mostly static content and not even a requirement of a backend (classic JAMstack). As a developer, you may have a blog where the content consists of a bunch of markdown files, that are part of the repo. So every time you write a new blog post, you just need to deploy to set it online. SSG is cheap to host.

A CMS backend is needed when a non-technical editor is supposed to edit contents. But what should happen when an editor changes the content of an article with a SSG system? The new content is available through the API, but not statically generated yet. It's possible to trigger new deployments after edits, but re-generation of a full website after a minor change is wasteful, fragile and slow.

### Server Side Rendered (SSR)

Server Side Rendering is a confusing term because it's not designating classical websites but a strategy to pre-render content on the server before the CSR kicks in (hydration). Search engine crawlers can parse it.

#### SSR hosting

SSR requires a Node.js runtime on the frontend stack server to query the backend to return HTML directly to the browser. That means you need two servers to host one website:

- Backend server provides the API
- Frontend server queries the API to return HTML

The frontend can not be hosted on the edge. It's good for SEO. Always creating pages from the source is slower than directly spitting out static pages.

### Incremental Static Regeneration (ISR)

ISR is one approach to solve shortcomings of SSR and SSG.

1. The first unlucky user vists a page that is outdated
2. The old static version is served first
3. The dynamic version kicks, with updated content (hydration)
4. The Node.js has detected old content server creates an updated static version
5. The next lucky visitor will be served the updated static content

#### ISR hosting

This of course also requires two servers for one website:

- Backend server provides the API
- Frontend server creates new static pages on the fly

The frontend however can still be hosted on the edge. It's good for SEO and it is fast. But it's more complex to setup too. It's also not the cheapest option.

## My takeaway

The JAMstack evangelists promise a fast future on the edge. The technology is genuinely impressive, yet complex. More moving parts means higher hosting costs. Think twice, not every project justifies this investment.

For small and mid-sized website projects, I still would recommend to explore server-side rendered PHP. It's faster to develop, easier to deploy, and more affordable to host. In my humble opinion, the simplicity often outweighs the architectural superiority that decoupled systems provide.

It's also a matter of personal preference, many full stack developers enjoy working with JavaScript these days.
