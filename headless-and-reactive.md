---
created: 2025-09-18 07:52:16
author: fl
title: Headless and reactive PHP
naviTitle: Headless and reactive PHP
navigation.excerpt: reactive websites with PHP and JS.
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

## Definition

The title might sound ominous, but in web development, "headless" and "reactive" are actually good. Let me explain how I use the words throughout the post.

### Headless

A software system where the front end (user interface) is separated from the back end (content management). That's well agreed upon.

### Reactive

A website that uses JavaScript to update parts of the page (via AJAX) by content coming from the server and by interaction of the user. This is my very own definition. Maybe it helps explaining what this is not.

- Not a static website, serving only full pages of HTML
- Not a classical serverful website, a server always renders a full page
- Not 'reactive web design', different website versions for each screen resolution

Got it? Good.

## How to choose

This is not about winners and losers. This is about team size, requirements and most of it all personal preference and skills. Many developers stick to their home stack. My observation:

- Backend-focused devs prefer to abstract frontend parts.
- Frontend-focused devs prefer to abstract backend parts.

## 1 - No reactivity

Check your premises. Do you really need a reactive website? Classical server side rendered websites are way less complicated to build, maintain, deploy and host. Server side rendered pages come with great SEO options. Specifically for small website projects, with smaller teams or even solo developers. Don't follow the latest trends without consideration.

For stateful elements or partial reactivity small drop-in JavaScript apps on a per page basis can work too.

## 2 - Decoupled

This dual stack approach consists of two independent systems that talk to each other.

- The PHP backend provides an API (REST, GraphQL).
- The frontend is based on JavaScript (Svelte, Next.js, Nuxt.js, Astro …)

Traditional PHP CMS systems bundle the backend and the frontend into one system. But a so called headless mode is now available for WordPress, Craft CMS and many more.

- [getkirby.com/…/headless-getting-started](https://getkirby.com/docs/cookbook/headless/headless-getting-started)
- [craftcms.com/…/graphql.html](https://craftcms.com/docs/getting-started-tutorial/more/graphql.html)
- [statamic.dev/rest-api](https://statamic.dev/rest-api)

PHP frameworks like Laravel and Symfony supprt API interfaces as well. The PHP backend system and the frontend system can live in separate codebases and can be developed and deployed independently. This makes it interesting for bigger teams or projects as well as frontend focused developers. The frontend website is just one client for the backend, another one might be a mobile app.

The use of Single Page Applications is a trend. Carefully consider if such a system is the best technology for the given project.

### Client Side Rendered (CSR)

This is the classical Single Page App (SPA) style. All the data is provided by the API to the frontend via AJAX calls. The website is constructed in the browser when a human visits.

### Server Side Generated (SSG)

During build time, usually during deployment, the whole frontend content is pre-rendered as static HTML pages. The initial load will display the static page (fast), then the SPA mode can serve every click from them then on.

### Server Side Rendered (SSR)

This mode is able to do both, classical server side rendering and client side rendering. It requires a Node.js runtime on the server to query the backend for the latest content to return HTML directly to the browser. The content is always fresh and it is good for SEO. Delivery might be slower than pre-rendered static pages.

There are plenty of additional strategies, like mixing the different methods together on a per-page basis or incrementally generating new content on intervals.

## 3 - Coupled

Some developers questioned the decoupled approach. Why not send HTML over the wire? Why not use existing tooling for routing and authentication? Modern PHP frameworks come with battle tested tooling. Twig and Blade are powerful templating languages. Why abandon all that? Build modern monoliths! This is faster and often easier to implement in terms of hosting and deployment as it involves fewer moving parts.

### A - Livewire

The aim of Laravel Livewire is to enable PHP developers to create modern reactive websites without having to leave the PHP world at all. The logic is written in PHP, while the templates are still in Blade, but with superpowers to enable live partial updates and reactivity.

- [laravel-livewire.com](https://laravel-livewire.com/)

### B - Inertia.js

Inertia.js, also hailing from the Laravel scene, has a different approach. It glues together the PHP backend with a JavaScript frontend, think Vue.js, React or Svelte based systems. Unlike with decoupled systems, the data is directly provided by the PHP layer, no need for an API. There is an adaptor for each JavaScript framework.

- [inertiajs.com](https://inertiajs.com/)

### C - Symfony UX

The user experience layer from Symfony is a mix of different technologies and boilerplate. It contains some ready made common use components for maps, icons and charts that can be directly used. Live components bring reactivity in a similar as Livewire. It also includes the Hotwire (37signals) modules Turbo and Stimulus.

- [ux.symfony.com](https://ux.symfony.com/)
- [hotwired.dev](https://hotwired.dev/)

#### AssetMapper

AssetMapper is PHP library used and recommended by Symfony to compile frontend assets in PHP, Node.js not required. It also acts like a kind of package manager and provides Twig tags to link to versionzed asset versions. The older alternative uses Webpack Encore. See [Symfony docs](https://symfony.com/doc/current/frontend.html#stimulus-symfony-ux-components).

### D - Others

Somehow also in this couple space are the following projects:

- [Sprig plugin for Craft CMS](https://putyourlightson.com/plugins/sprig) - based on HTMX
- [YoYo](https://getyoyo.dev/) - based on HTMX

## SEO

For many web projects good visibility in search engines is a must. Search crawlers may not interpret JavaScript. That boils down to:

- ❌ Single Page Application with CSR, bad SEO
- ✅ Classical PHP with no reactivity, good SEO
- ✅ The static sites rendered by SSG, good SEO
- ✅ Sever side rendered pages of SSR, good SEO

## Deployment and hosting

How can the different options be put on public server in an automated way? This is a wide subject, let's focus on the requirements for the above mentioned reactive PHP projects.

### No reactivity

Easy peasy. This type does not require any complex interaction between frontend and backend and therefore is easy to deploy to a web host that supports PHP.

### Decoupled

For the decoupled project, the individual parts can be deployed to different web hosts:

- PHP backend: a service that has a PHP runtime.
- JS frontend: a dedicated JAMstack hosting service.

This is sophisticated, but also a bit complex. Depending on the project requirements and the service features, it might also be possible to deploy both projects to a single hosting service.

#### Regeneration of SSG

What happens when an editor changes the content of an article with a server side generated pages? The new content is available through the API of the backend and thus can be shown to users. But for SEO purposes, there should also be a statically generated version of that content.

Re-generation of a full website after a minor change is wasteful, fragile and slow.

To solve this issue another acronym was invted: ISR. It stands for Incremental Static Regeneration. On user request, the frontend checks if a cached static version exists, if not regenerate one (first unlucky user). That means the previously cheap static hosting option suddenly needs to do some sort of server side rendering too (more $$$). The JavaScript framework also needs to support that mode. Probably not surprising, Next.js is good at that.

A different approach also related to this was pioneered by Astro: [Dynamic islands](https://docs.astro.build/en/concepts/islands/), where only parts of the page are defined as dynamic.

### Coupled

With the modern monoliths the frontend and the backend code are usually deployed alongside.

- The frontend part needs to be compiled during deployment.
- A Node.js runtime is required to serve the server side generated parts.

The first version of [new platform](https://new.fortrabbit.com) will already support many of the above mentioned workflows.

### Hosting requirements

| Type             | Node.js runtime `*` | Node.js via PHP `**` | Node.js deployment `***` |
| ---------------- | ------------------- | -------------------- | ------------------------ |
| No reactivity    | No                  | No                   | No                       |
| Decoupled        | Yes                 | No                   | Yes                      |
| Inertia.js       | No                  | Yes                  | Yes                      |
| Laravel Livewire | No                  | No                   | No                       |
| Symfony UX       | No                  | No                   | [Optional](#assetmapper) |
| Sprig (Craft)    | No                  | No                   | No                       |
| Yoyo             | No                  | No                   | No                       |

#### Legend

- `*` Node.js runtime - `npm run serve`
- `**` Node.js via PHP - PHP talks to a backend Node.js process (worker)
- `***` Node.js deployemnt - `npm run build` to generate artifacts
