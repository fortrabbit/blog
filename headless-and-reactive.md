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
      content: 'JAMstack, react, vue, php, ajax, fullstack'
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

// Not sure about this part. "abstract"? What does it mean exactly?
- Backend-focused devs prefer to abstract frontend parts.
- Frontend-focused devs prefer to abstract backend parts.

## 1 - No reactivity

Check your premises. Do you really need a reactive website? Classical server side rendered websites are way less complicated to build, maintain, deploy and host. Server side rendered pages come with great SEO options. Specifically for small website projects, with smaller teams or even solo developers. Don't follow the latest trends without consideration.

// Not sure about stateful here. What does it mean exactly?
For stateful elements or partial reactivity small drop-in JavaScript apps on a per page basis can work too.

## 2 - Single Page Applications

This dual stack approach consists of two independent systems that talk to each other.

- The PHP backend provides an API (REST, GraphQL).
- The frontend is based on JavaScript (Svelte, Next.js, Nuxt.js, Astro …)

Traditional PHP CMS systems bundle the backend and the frontend into one system. But a so called headless mode is now available for WordPress, Craft CMS and many more.

- [getkirby.com/…/headless-getting-started](https://getkirby.com/docs/cookbook/headless/headless-getting-started)
- [craftcms.com/…/graphql.html](https://craftcms.com/docs/getting-started-tutorial/more/graphql.html)
- [statamic.dev/rest-api](https://statamic.dev/rest-api)

PHP frameworks like Laravel and Symfony support API interfaces as well. The PHP backend system and the frontend system can live in separate codebases and can be developed and deployed independently. This makes it interesting for bigger teams or projects as well as frontend focused developers. The frontend website is just one client for the backend, another one might be a mobile app.

The use of Single Page Applications is a trend. Carefully consider if such a system is the best technology for the given project.

### Client Side Rendered (CSR)

This is the classical Single Page App (SPA) style. All the data is provided by the API to the frontend via AJAX calls. The website is constructed in the browser when a human visits.

### Server Side Rendered (SSR)

This mode allows to get the advantages of both classical sever side rendering and client side rendering. The browser receives a page ready to be rendered, and the JS framework can then take over. This has important benefits: the browser can act quicker and search engine's crawlers can easily parse it, making it great for SEO. On the other hand, it requires a Node.js runtime on the server to query the backend to return HTML directly to the browser.

There are plenty of additional strategies, like mixing the different methods together on a per-page basis or incrementally generating new content on intervals.

## 3 - API-less stacks (?) / Integrated stacks (?) / Monolithic interactivity (?: my preferred one, here, probably)

Some developers questioned the decoupled approach of having to build an API to talk to the frontend. Why not send HTML over the wire? Why not use existing tooling for routing and authentication? Modern PHP frameworks come with battle tested tooling. Why abandon all that? Build modern monoliths! This is faster and often easier to implement in terms of hosting and deployment as it involves fewer moving parts.

### A - Livewire

The aim of Laravel Livewire is to enable PHP developers to create modern reactive websites without having to leave the PHP world at all. The logic is written in PHP, while the templates are still in Blade, but with superpowers to enable live partial updates and reactivity.

- [laravel-livewire.com](https://laravel-livewire.com/)

### B - Inertia.js

Inertia.js, also hailing from the Laravel scene, has a different approach. It glues together the PHP backend with a JavaScript frontend, think Vue.js, React or Svelte based systems. Unlike with decoupled systems, the data is directly provided by the PHP layer, no need for an API. There is an adaptor for each JavaScript framework.

Inertia also supports SSR (Server Side Rendering) strategy, but it then requires a nodeJS runtime running alongside PHP.

- [inertiajs.com](https://inertiajs.com/)

### C - Symfony UX

The user experience layer from Symfony is a mix of different technologies and boilerplate. It contains some common components for maps, icons and charts that can be directly used. Live components bring reactivity in a similar way as Livewire. It also includes the Hotwire (37signals) modules Turbo and Stimulus.

- [ux.symfony.com](https://ux.symfony.com/)
- [hotwired.dev](https://hotwired.dev/)

### D - Others

[HTMX](https://htmx.org) is a bit different than the previous examples: it's a backend-agnostic JavaScript library allowing developers to send HTML over the wire. It has become quite popular these last years and can add reactivity here and there without too much change on the backend side.

Somehow also in this couple space are the following projects:

- [Sprig plugin for Craft CMS](https://putyourlightson.com/plugins/sprig) - based on HTMX
- [YoYo](https://getyoyo.dev/) - based on HTMX

## SEO

For many web projects good visibility in search engines is a must. Search crawlers may not interpret JavaScript. That boils down to:

- ❌ Single Page Application with CSR, bad SEO
- ✅ Classical PHP (or static sites) with no reactivity, good SEO
- ✅ Sever side rendered pages of SSR, good SEO

## Deployment and hosting

How can the different options be put on public server in an automated way? This is a wide subject, let's focus on the requirements for the above mentioned reactive PHP projects.

### No reactivity

Easy peasy. This type does not require any complex interaction between frontend and backend and therefore is easy to deploy to a web host that supports PHP.

### Single Page Applications

For the decoupled project, the individual parts can be deployed to different web hosts:

- PHP backend: a service that has a PHP runtime.
- JS frontend: a dedicated JAMstack hosting service.

This is sophisticated, but also a bit complex. Depending on the project requirements and the service features, it might also be possible to deploy both projects to a single hosting service.

### Monolithic Reactivity

With modern monoliths, the frontend and the backend code are usually deployed alongside. The frontend part usually needs to be compiled during deployment (which requires node on the build system).

If SSR is used (through Inertia, for example), node is also required on the machine hosting the app.

// Which ones? We should tell people. Otherwise it's confusing.
The first version of [new platform](https://new.fortrabbit.com) will already support many of the above mentioned workflows.

### Hosting requirements

| Type             | Node.js runtime `*` | Node.js via PHP `**` | Node.js deployment `***` |
| ---------------- | ------------------- | -------------------- | ------------------------ |
| No reactivity    | No                  | No                   | No                       |
| Classical SPA    | No                  | No                   | Yes                      |
| Inertia.js       | No                  | Yes                  | Yes                      |
| Inertia.js (SSR) | No                  | Yes                  | Yes                      |
| Laravel Livewire | No                  | No                   | Yes                      |
| Symfony UX       | No                  | No                   | [Optional](#assetmapper) |
| Sprig (Craft)    | No                  | No                   | No                       |
| Yoyo             | No                  | No                   | No                       |
| HTMX             | No                  | No                   | No                       |

#### Legend

- `*` Node.js runtime - `npm run serve`
- `**` Node.js via PHP - PHP talks to a backend Node.js process (worker)
- `***` Node.js deployemnt - `npm run build` to generate artifacts

## Server Side Generation (SSG)?

We have not talked about SSG in this article, because it's not directly related to the interaction between PHP and JS, but we might cover this in a future article. There is indeed a lot to talk about, regarding deployment strategies.
