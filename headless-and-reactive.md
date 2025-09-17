---
created: 2025-09-16 14:52:02
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
      content: 'JAMstack, react, vue, php, ajax, async, promise, stateful'
---

This is a opinionated view from my angle of the web in 2025. It helps me thinking about the subject, since we wan't to cover a lot of this with our [new hosting platform](https://new.fortrabbit.com).

The title might sound ominous, but in web development, "headless" and "reactive" are actually good.

## How to choose

This is not about winners and losers. This is about team size, requirements and most of it all personal preference and skills. Many developers stick to their home stack.

- Some PHP developers tend towards backend development and try to avoid too much frontend work. Don't need to leave PHP? Great!
- Others feels the need to control the border radius and the shade of blue. Don't need to leave JS? Great!

## 1 - No reactivity

Check your premises. Do you really need a reactive website? Classical server side rendered websites are way less complicated to build, maintain, deploy and host. Server side rendered pages come with great SEO options. Specifically for small website projects, with smaller teams or even solo developers. Don't follow the latest trends without consideration. You may still add on-page JavaScript to compute stuff without querying the server.

For partial reactivity (stateful) small drop-in Javascript apps on a per page basis can work too.

## 2 - Decoupled

This dual stack approach consists of two independent systems that talk to each other.

- The PHP backend provides an API (REST, GraphQL).
- The frontend is based on Javascript (Svelte, Next.js, Nuxt.js, Astro, HTMX …)

Traditional PHP CMS systems bundle the backend and the frontend into one system. But a so called headless mode is now available for WordPress, Craft CMS and many more.

- [getkirby.com/…/headless-getting-started](https://getkirby.com/docs/cookbook/headless/headless-getting-started)
- [craftcms.com/…/graphql.html](https://craftcms.com/docs/getting-started-tutorial/more/graphql.html)
- [statamic.dev/rest-api](https://statamic.dev/rest-api)

PHP frameworks like Laravel and Symfony support API interfaces for a long time. The PHP backend system and the frontend system can live in separated code bases and can be developed and deployed independently. This makes it interesting for bigger teams or projects as well as frontend focused developers. The frontend website is just one a for the backend, another one might be a mobile app.

The use of Single Page Applications is a trend. Carefully consider if such a system is the best technology for the given project.

### Client Side Rendered (CSR)

This is the classical Single Page App (SPA) style. The frontend consists of logic to render templates. All the data is provided by API to the frontend via AJAX calls. The website is constructed in the browser when a human visits.

### Server Side Generated (SSG)

During build time, usually during deployment, the whole content is pre-rendered as static HTML pages. The initial load will display the static page (fast), then the SPA mode will serve every click from them then on.

### Server Side Rendered (SSR)

This mode is able to do both, classical server side rendering and client side rendering. It requires a Node.js runtime on the server to query the backend for the latest content to return HTML directly to the browser. The content is always fresh and it is good for SEO. Delivery might be slower than pre-rendered static pages.

There are plenty of additional strategies, like mixing the different methods together on a per-page basis or incrementally generating new content on intervals.

### Git repo organization

How to structure the code, setup local development and finally deploy to a public host?

- **Monorepo:** the frontend and the backend code. This is easier to share and demo. The [Craft CMS Nuxt starter](https://github.com/craftcms/starter-nuxt) is an example.
- **Polyrepo:** Frontend and backend code are in different repos. For larger teams, separated code bases might be interesting.

## 3 - Coupled

Some developers questioned the decoupled approach. Why not send HTML over the wire? Why not use existing tooling for routing and authentication? Modern PHP frameworks come with battle tested tooling, like routing and authentication. Twig and Blade are powerful templating languages. Why abandon all that? Build modern monoliths! This is faster and often easier to implement in terms of hosting and deployment as it involves fewer moving parts.

### A - Livewire

The aim of Laravel Livewire is to enable PHP developers to create modern reactive websites without having to leave the PHP world at all. The logic is written in PHP, while the templates are still in Blade, but with superpowers to enable live partial updates and reactivity.

- [laravel-livewire.com](https://laravel-livewire.com/)

### B - Interia.js

Interia.js, also hailing from the Laravel scene, has a different approach. It glues together the PHP backend with any Javascript frontend, think Vue.js or React based systems. Unlike with decoupled systems, the data is directly provided by the PHP layer. Each Javascript framework has it's own adaptor.

- [inertiajs.com](https://inertiajs.com/)

### C - Symfony UX

The user experience layer from Symfony is a mix of different technologies and boilerplate. It contains some ready made common use components for maps, icons and charts that can be directly used. It also includes the Hotwire (37signals) modules Turbo and Stimulus.

- [ux.symfony.com](https://ux.symfony.com/)
- [hotwired.dev](https://hotwired.dev/)

### D - Others

Somehow also in this couple space (I guess) are the following projects:

- [Sprig plugin for Craft CMS](https://putyourlightson.com/plugins/sprig) - based on HTMX
- [reactphp.org](https://reactphp.org/) - Event-driven, non-blocking I/O with PHP
- [getyoyo.dev](https://getyoyo.dev/) - based on HTMX
- [Framework X](https://framework-x.org/) - based on ReactPHP
- [github.com/ReactiveX/RxPHP](https://github.com/ReactiveX/RxPHP)

## SEO

Not for all, but for many web projects good visibility in search engines is a must. One has to assume that seach engine crawlers will not be able to intepret Javascript like a browser.

The Singe Page Application with CSR will be invisible for the search engines.

With SSG, all pages are pre-rendered and the SPA mode kicks in when a human visitor stops by. But if an editor changes the content of an article? Usually the generation of the pages pnly happens when teh project get's deployed. With deploy webhooks, deployment, even incremental ones can be trigged, but that setting up such system can be challenging.

Classical PHP with no reactivity, SSR and coupled projects all come with good SEO.

## Deployment and hosting

How can the different options be put on public server in an automated way? This is a wide subject, let's focus on the requirements for the above mentioned reactive PHP projects.

### No reactivity

Easy peasy. This type does not require any complex interaction between frontend and backend and therefore is easy to deploy to a web host that supports PHP.

### Decoupled

For the decoupled project, the frontend and the backed projects can be deployed to different web hosts.

- Deploy the PHP part to service that has a PHP runtime.
- Deploy the JS part to a dedicated JAMstack hosting service.

This is sophisticated, but also a bit complex. Depending on the project requirements and the service features, it might also be possible to deploy both projects to a single hosting service.

In most cases the frontend part needs to be built using something like `npm run build`. This is usually done during deployment. For example with GitHub Actions or a PaaS service that connects to the Git repo and offers build steps.

### Coupled

With the modern monoliths the frontend and the backend code are usually deployed alongside.

- The frontend part needs to be compiled during deployment.
- A Node.js runtime is required to serve the server side generated parts.

The first version of [new platform](https://new.fortrabbit.com) will already support many of the above mentioned workflows.

### Hosting requirements

| Type              | Node.js runtime `*` | Node.js via PHP `**` | Node.js deployment `***` |
| ----------------- | ------------------- | -------------------- | ------------------------ |
| No reactivity     | No                  | No                   | No                       |
| Decoupled         | Yes                 | No                   | Yes                      |
| Inertia.js        | No                  | Yes                  | Yes                      |
| Laravel Livewire  | No                  | No                   | No                       |
| Symfony UX        | No                  | No                   | ?                        |
| Sprig (Craft CMS) | No                  | No                   | No                       |
| ReactPHP          | ?                   | ?                    | ?                        |
| Yoyo              | No                  | No                   | No                       |
| Framework X       | No                  | No                   | No                       |

#### Legend

- `*` Node.js runtime - `npm run serve`
- `**` Node.js via PHP - PHP talks to a backend Node.js process (worker)
- `***` Node.js deployemnt - `npm run build` to generate artifacts
