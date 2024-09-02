---
author: fl
created: 2024-05-17
title: How we chose our new frontend stack
intro: So many options - React, Svelte, Vue, Nuxt, htmx, Interia, Livewire. What to choose for our new web properties?
figure:
  src: frontend-stack-poster.png
tag:
  - webdev
---

We are currently building a [new platform](https://new.fortrabbit.com) version (big rewrite). This includes our customer facing web properties: dashboard (hosting control panel), marketing page, docs and a blog. As a PHP hosting service we were curious to dog-food ourselves a new PHP-friendly frontend tech stack. This is what we have now and why.

Our current web properties are already a decade old. They run as independent applications. Web, blog and docs are based on the Slim framework. The hosting dashboard is made with Laravel. It talks to a private API, also based on Laravel. I enjoyed using the powerful [Twig templating](https://twig.symfony.com/) engine across those properties. jQuery was used for interactivity and I created a global CSS stylesheet to be linked from all websites to align the visual appearance.

Obviously in 2022 (when we started the new platform), we would do things a bit differently.

At first we looked at a middleware solution between frontend and PHP. [Livewire](https://livewire.laravel.com/) (by Caleb Porzio) was just getting more integrated in the Laravel eco system. Although sexy, conceptually [Intertia.js](https://inertiajs.com/) (by Jonathan Reinink) was closer to our philosophy.

We already had build a dashboard click dummy built in [Nuxt.js](https://nuxt.com/) (as a convenience layer for Vue.js). Originally we planned to start from scratch for the real thing with an eye on Svelte, maybe HTMX and raw web components. But we realised that Nuxt.js was actually matching our requirements and it was easier to just iterate on the existing code base from the dummy. The [Nuxt Content](https://content.nuxt.com/) extension serves the markdown files for the blog and the docs. The dashboard is a SPA, while the other websites will be pre-rendered.

The code for our web properties now lives in a mono repo, handled with `pnpm`. The Vue components library is shared between the different projects.

We tried [Storybook](https://storybook.js.org/) and [Histoire](https://histoire.dev/) to build and test our components in isolation. But I kept iterating on the components within their original context so the stories got outdated quickly. So we ditched that idea for now.

We also swapped my [home-brew CSS solution Teutonic in favor for Tailwind](https://medium.com/teutonic-css/retiring-my-own-little-css-framework-e0a130ca2a33). I am still not sure if that is really a win, but maybe that's just my hurt ego.

Later down the line we also decided to have the frontend talk to the backend API directly, instead of an additional PHP layer (Interia.js).

For the API we flirted with GraphQL for a second but then quickly turned back to build a classical REST API. This is our PHP layer finally. It's build with the [API Platform](https://api-platform.com/) (Symfony world).

It took me a while to adapt to some of the modern paradigms. I sometimes miss my old simple tech. But maybe that's just because I am getting old. A Single Page Application is nice, but loading traditional pages rendered by the PHP server from a monolith application served us well for a long time.

Having customer facing technology separated from backend logic is a good separation of concerns. Yet separated code bases in different programming languages are more complex. We have more specific domain knowledge now.
