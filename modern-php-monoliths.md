---
created: 2025-11-04 08:15:51
author: fl
title: Modern PHP monoliths
naviTitle: Modern PHP monoliths
intro: Coupled websites with PHP and JS.
lead: Web pages are so yesterday. Single-page apps are the shit. Users want interactive experiences. But you don't have to get headless right away. This is an introduction to coupled systems with PHP and JavaScript.
wip: true
tag:
  - opinion
figure:
  src: monolith-poster.png
  # emoji: 🗿 🗿 🐘 🗿
  # color: rgba(185, 202, 232, 1)
head:
  meta:
    - name: 'keywords'
      content: 'JAMstack, react, vue, php, ajax, async, promise, stateful, fullstack, XHR'
---

## What's a modern monolith?

The cool kids create headless systems, where frontend and backend are fully separated, loosely connected by an API. See our [headless PHP](/headless-php) post on decoupled systems with PHP.

But some developers questioned decoupled headless systems. Why not use existing tooling? Or why not even send HTML over the wire? The author of Inertia.js describes his idea like so:

:Quote{text="Transparency. Observability. Accountability."}{ author="Jonathan Reinink" text="It allows developers to build rich single-page client-side apps, without having to build a full REST or GraphQL API, or learn client-side state management, routing, and really much of what comes with modern SPAs." }

One benefit is making use of the battle-tested tooling that comes with modern PHP frameworks and CMS: routing, authentication, ORM. The other is that such systems are easier to set up, host and deploy: one codebase and one hosting environment.

## Architecture

Unlike headless systems, modern monoliths are coupled together. There are different approaches to do this.

- Magic: Freeing backend-oriented developers from dealing with JavaScript.
- Glue: Connecting frontend and backend, removing the API requirement.

### A - Livewire

The aim of Laravel Livewire is to enable PHP developers to create modern reactive websites without having to leave the PHP world at all. The logic is written in PHP, while the templates are also still in Blade, but with superpowers to enable live partial updates and reactivity.

- [laravel-livewire.com](https://laravel-livewire.com/)

### B - Inertia.js

Inertia.js, also hailing from the Laravel scene, has a different approach. It glues together the PHP backend with a JavaScript frontend, think Vue.js, React or Svelte based systems. Unlike with decoupled systems, the data is directly provided by the PHP layer, no need for an API. There is an adaptor for each JavaScript framework.

Inertia supports SSR (Server Side Rendering), but it requires a Node.js runtime running alongside PHP.

- [inertiajs.com](https://inertiajs.com/)

### C - Symfony UX

The user experience layer from Symfony is a mix of different technologies and boilerplate. It contains some common components for maps, icons and charts that can be directly used. Live components bring reactivity in a similar way as Livewire. It also includes the Hotwire (37signals) modules Turbo and Stimulus.

- [ux.symfony.com](https://ux.symfony.com/)
- [hotwired.dev](https://hotwired.dev/)

#### AssetMapper

AssetMapper is a PHP library used and recommended by Symfony to compile frontend assets in PHP - Node.js not required. It also acts like a package manager and provides Twig tags to link to versioned asset versions. The older alternative uses Webpack Encore. See [Symfony docs](https://symfony.com/doc/current/frontend.html#stimulus-symfony-ux-components).

### D - Datastar

Datastar is a new framework, which is primarely a small JavaScript library that can be pulled in by CDN. It's backend agnostic and has connectors (SDKs) to Laravel, Craft CMS and others already. It has a paid Pro version and it claims to solve more problems than it creates.

- [data-star.dev](https://data-star.dev)

### E - HTMX and derivates

[HTMX](https://htmx.org) and [Unpoly](https://unpoly.com/) are also a backend-agnostic JavaScript libraries, adding reactivity without too much change on the backend side. Too dive even deeper, have a look at [Hypermedia Systems](https://hypermedia.systems/) - a book that it looks at HTMX and Hyperview.

Somehow also in this space are the following projects:

- [Sprig plugin for Craft CMS](https://putyourlightson.com/plugins/sprig) - based on HTMX
- [YoYo](https://getyoyo.dev/) - based on HTMX
- [Nuxt Kirby](https://nuxt-kirby.byjohann.dev/) - data bridge for Kirby CMS and Nuxt, headless + monolith

## My takeaway

Modern monoliths are a great alternative to [headless systems](/headless-php.md) and an improvement over classical page by page websites.

This is not about winners and losers. This is about team size, requirements and most of it all personal preference and skills. Many developers stick to their home stack. My observation:

- Backend-focused devs try to get away without too much frontend.
- Frontend-focused devs try to get away without too much backend.

That's why specifically the magic systems are attractive to backend-focused developers.

We are currently building our [new platform](https://new.fortrabbit.com). One of the next features we want to add is Node.js that can be called through PHP (on a worker job), required to make Inertia.js work with SSR mode.

---

## Appendix

| System           | Type  | Node.js via PHP `*` | Node.js deployment `**`  |
| ---------------- | ----- | ------------------- | ------------------------ |
| Laravel Livewire | Magic | No                  | No                       |
| Inertia.js       | Glue  | Yes                 | Yes                      |
| Symfony UX       | Magic | No                  | [Optional](#assetmapper) |
| Datastar         | Magic | No                  | No                       |
| Sprig (Craft)    | Magic | No                  | No                       |
| Yoyo             | Magic | No                  | No                       |

### Legend

- `*` Node.js via PHP - PHP talks to a backend Node.js process (worker)
- `**` Node.js deployment - `npm run build` to generate artifacts
