---
author: fl
title: PHP & JS?
created: 2024-06-24
intro: Is something missing to bring together JS and PHP?
lead: Is something missing to bring together JS and PHP?
figure:
  src: php-js-poster.png
tag:
  - opinion
---

Maybe I am not the best to judge here. I am not even a real developer. My role is more product ownership and design. But I wonder about the relation of PHP and JavaScript for 2024 and beyond. For a PHP hosting provider, that's an important question.

A decade ago, we at fortrabbit were excited by recent improvements in PHP and its ecosystem - specifically Composer. PHP evolved beyond a Pretty HomePage language for simple websites into something you can build web applications with. Symfony and Laravel are great frameworks for that. Yet, we are still hosting more PHP websites than web applications today.

Most websites here are build with a CMS system. Although those come in different flavours ([Craft CMS](https://craftcms.com/), [Statamic](https://statamic.com/), [Kirby](https://getkirby.com/), WordPress …), they can all use PHP to calculate something on the server side and spit out some HTML to the browser.

It's a simple concept and maybe that's why it is so powerful. It's not prefect, but it works surprisingly well (SEO included), when done right. Templating engines like Blade and Twig make it fun to create views. So from my point of view: LAMP stack still rocks!

But than there is the JS part and the CSS styles, for which you will usually want to have some tooling to compress the authoring files into production code. I don't know anyone doing that with PHP today. So somehow, you need to integrate some JavaScript tooling like Vite into your workflow. I don't ‘feel' the connection here.

There is Livewire and Interia.js, both projects aim to minimize the gap between the JS and the PHP world. We looked into those, but for our new platform we settled with a JavaScript setup for all frontend properties (see [blog post](https://blog.fortrabbit.com/our-new-frontend-stack)). It felt more natural to not mix the eco systems.

There recently was some PHP vs JS discussion going on. Polarisation helps getting attention:

- Theo: [Why Don't We Have A Laravel For JavaScript?](https://www.youtube.com/watch?v=yaodD79Q4iE)
  - TLDR; Because we don't want to be such a closed eco system.
- Aaron Francis: [Laravel vs React](https://www.youtube.com/watch?v=gRtv-BVkwA4)
  - A primer on the technical foundations and options frontend / backend
  - TLDR; It's not ‘VS' it's ‘AND', bind them with Intertia or LiveWire
  - Also much longer: [Mostly technical podcast with Taylor Otwell](https://www.youtube.com/watch?v=NC6h1Oaz1rM)

Let's have a look what Craft CMS is doing. Craft CMS is a classical LAMP stack CMS with Twig templating. But it also offers a headless mode. The backend is a PHP application running on a PHP hosting service like ours, serving the GraphQL API and the control panel to edit content. The frontend is usually a JAM stack based application consuming GraphQL to display dynamic content from the database.

That's great. But it is also more complex than doing it the old fashioned way. You probably need to have two hosting setups, one for the backend CMS, one for the frontend. Not all Craft CMS plugins will work with JAM stack frontends. GraphQL is a powerful weapon, it's easy to crash the server with it. There are all kind of extra considerations. Exchanging with our customers in support about Craft CMS with GraphQL shows me all the challenges. It's not that easy.

Statamic was a flat file CMS and turned into ~~jack of all trades~~ a super versatile tool: Beside direct static file output, it supports a database and a headless mode.

I would like to see ‘PHP AND JS' as well. But I am not sure if the current answers are enough. It seems to me that the JS world is currently extending classical flat file Jamstack apps by more dynamic features (server side rendering to some extend).

We have been discussing ideas to provide hosting for JavaScript based applications for almost a decade. So far we have been hesitant. Everything in JS world is changing so fast. Putting out a service means commitment for many years. For the new platform we will start by providing integrated tooling to run `npm` tasks during deployment for all kind of build processes. We are also exploring ideas to include a Node.js runtime available with the apps (early stages).

Please don't hesitate to share your requirements and use cases with us. We are eager to learn.

In the meantime let me reminiscence about the good old simple web and pretty home pages. I recently stumbled over [Textpattern](https://textpattern.com/) and [Moveable Type](https://movabletype.org/). It's great to see that both are still around.
