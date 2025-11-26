---
created: 2025-11-26 10:24:14
author: fl
title: New platform public BETA
naviTitle: New platform public BETA
intro: A new hosting experience at your fingertips
lead: Welcome to the public BETA of our new platform.
tag:
  - changelog
  - chronicles
figure:
  emoji: 👯‍♀️👯‍♂️
  color: rgba(255, 225, 0, 1)
  textColor: rgba(155, 125, 0, 1)
  text: We are so thrilled to share this.
links:
  - title: New platform BETA details
    route: /platform/new/beta
    property: docs
head:
  meta:
    - name: 'keywords'
      content: 'fortrabbit, new platform, beta, PHP hosting, GitHub integration, multi-staging'
---

It's been years in the making: thousands of tickets, countless cups of coffee, endless debates about tiny details. Now we are finally ready. This is not just another update. We built something entirely new from scratch. We **completely redefined** our optimal vision of PHP hosting. It's a big bet. Fingers crossed you like it. 🤞

## What is fortrabbit anyhow?

Inspired by the original Heroku PaaS: a hosting platform to deploy modern PHP websites and web applications. It's apps, not servers; it integrates GitHub, runs on AWS, and won't break your bank. It encourages best practices, but doesn't judge you when you ignore them. It's a good fit for modern PHP-based websites and web applications built with Craft CMS, Kirby, Statamic, Laravel, Symfony, and many more.

- **Intuitive dashboard** that gets out of your way
- **Persistent storage** with direct SSH/SFTP access
- **Component based pricing** to individually book and scale parts
- **Workers** offload tasks to the background
- **Free trial** available for each new app
- **Transparent pricing** with component-based model
- **No setup fees** or hidden costs
- **Pay-as-you-scale** philosophy
- **GitHub signup**
- **Connect any GitHub repository** git push to deploy
- **Build pipeline** with Node.js support during deployment
- **Multi-environment staging** with branch-based environments
- **SSH key-only authentication** for better security
- **Key-value store** (coming soon)

## Why a BETA for a hosting service?

I've written about our [decision to do a big rewrite](/yes-we-rewrite.md) before. We needed a complete overhaul. We've been working on the new platform for years. It became our home and we quite like it. It's time now. While we are still polishing some edges and adding features, the core experience are ready.

:ContentQuote{text='There is no test like production.'}

Opening it up is exciting, but also a bit scary. We are stepping out of our comfort zone to see how you interact with the platform. It's already a significant upgrade over the old platform. It's ready for action.

- **Now open to everyone**
- It's paid. We are confident in the value it provides.
- [See all BETA details](https://docs.fortrabbit.com/platform/new/beta)

## New design

Building on the existing brand, the design language got an update. We still use the old logo; colors and typography have been refreshed. We hope you like. You are looking at it now. [Goodbye old design](/goodbye-hello.md).

## Updated web properties

Our websites have been updated. Communication is mostly about the new platform. But the old platform is not going anywhere soon. Both systems will run [side by side](#no-rush-for-existing-clients) for a long time.

### New platform access

- [dash.fortrabbit.com](https://dash.fortrabbit.com) - new dashboard
- [docs.fortrabbit.com](https://docs.fortrabbit.com) - new docs
- [www.fortrabbit.com](https://www.fortrabbit.com) - new marketing (replaced old)
- [blog.fortrabbit.com](https://blog.fortrabbit.com) - new blog (replaced old)

### Old platform access (unchanged)

Existing customers can still continue to use the old system as usual. See [new and old side by side](#no-rush-for-existing-clients).

- [dashboard.fortrabbit.com](https://dashboard.fortrabbit.com) - old dashboard
- [help.fortrabbit.com](https://help.fortrabbit.com) - old help

## New pricing

When the service was launched 13 years ago, our vision was to raise awareness among developers that hosting is not just about getting more horsepower per dollar. Our aim was — and still is — to create an understanding of the value of a managed hosting service. It's not the cheapest service, but if you are using it professionally, you can easily afford it.

That turned out to be a tough sell. Web hosting is still mostly considered a commodity. We also saw the understandable wish from developers to host many small websites, like:

- Fun, personal, weekend projects
- Small client projects
- Staging environments

Unlike with a VPS, where you have one server to cram with your projects, fortrabbit uses dedicated resources for each environment. This is, we believe, the better but also more expensive route.

So, one of the design goals was to come up with more affordable pricing. It was also a requirement to create an entirely new platform. A Herculean task against all odds. So much of a product is pricing.

### Infrastructure

I am very proud of the work the infrastructure team has done in this area. We have been able to cut down our reliance on AWS, enabling us to revisit the infrastructure provider question later. For now, we found creative ways (and hacks) to keep AWS costs low.

- More intelligent allocation and redistribution
- Better resource utilization

### Pricing structure

We also looked at pricing from the product view. The old platform has three easy-to-understand plans. While this helps with cognitive load, it's also wasteful. We adapted the component pricing of the former Pro Stack for the new platform.

- XS plans: little resources, but affordable
- Component-based: pay only for tech you need
- Easy scaling: pay only for resources you need

To make things easier, we included different pricing presets for software. When booking a flat-file system that does not require a database (Kirby, Statamic, Grav …), the MySQL component is not pre-selected. When booking software that requires more resources, we suggest that right away.

In addition, there are [pricing examples](https://www.fortrabbit.com/pricing#examples) showcasing use cases with multiple environments.

We also removed the old company plans because they often confused customers.

### Pricing state

In total, you'll get much more performance for the same price with the new platform, and there are also additional smaller plans.

This will enable many more interesting use cases. We are curious to see how the new pricing will be perceived, specifically the component based pricing is a bet.

See our new [cost breakdown](https://www.fortrabbit.com/us/cost-breakdown) to get an idea about our spending.

### Pricing outlook

We still need to gather more experience with performance running more environments. So pricing is also subject to change.

## New docs

We take customer education and self-service seriously: there are now about 300 articles with a total of ~80,000 words and ~560,000 characters. It's based on the current help pages but significantly updated. You don't need to read it all to get the platform. It's just there.

The documentation is human-written (with some help from AI), well-structured, curated, and maintained. It's easily accessible, searchable, and designed to be easy to read and parse. It's also well-linked from the new dashboard: The little `[i]` icons provide inline help as well as links to relevant articles.

## New legal section

We have reviewed and extended our legal center. The new legal docs are applicable for all existing and new customers, covering the old and the new platform. The updates are done for clarify.

- [fortrabbit.com/legal](https://www.fortrabbit.com/legal) - New legal center
- [github.com/fortrabbit/legal](https://github.com/fortrabbit/legal) - Legal docs with full changelog

## No rush for existing clients

The old platform continues to run in parallel, giving you plenty of time. We'll support you hands-on with the migration when you are ready.

- **Side-by-side operation** - both platforms will run in parallel
- **Self-service migration** for early adopters
- **Assisted migration program** planned for later

- [New and old](https://docs.fortrabbit.com/platform/new/new-and-old): side by side
- [Changes](https://docs.fortrabbit.com/platform/new/changes): old and new platform compared
- [Migration](https://docs.fortrabbit.com/platform/new/migration): timing and details

## What's next?

This BETA launch is just the beginning. We've got a full backlog. Next, we are working to make it feature-complete and even more robust by hosting more production websites and web applications. From that list:

- Live server metrics in the dashboard
- Live logging in the dashboard
- Live event log in the dashboard
- Event notification system
- Extended collaboration
- Key-value store

It will take a while until everything will come available. The next step is general availabilty. As usual, we are conservative about timing, we look forward to remove the BETA flag in 2026.

### PHP 8.5(.1)

We are preparing for PHP 8.5 and will roll it out as soon as all supported extensions are updated and tested. We want to ensure a smooth transition, so we'll likely release it with the first dot version.

## We want your feedback

Don't just sit here. Deploy something!

- [Signup](https://dash.fortrabbit.com/signup) - start your first free trial
- [Explore the documentation](https://docs.fortrabbit.com/platform/new)

Found a bug? Have a feature request? Love something? Hate something? We want to hear about all of it. Start a chat using the chat bubble or email us at [support@fortrabbit.com](mailto:support@fortrabbit.com).

## Thanks

Thank you to everyone who made this possible - our incredible team, our patient alpha testers, and our loyal existing customers. It's a big drop for us. It's so many things. When it works out well, magic happens and the service becomes more than just the sum of its parts.

Here's to the next chapter of fortrabbit. 🚀
