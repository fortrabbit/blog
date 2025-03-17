---
title: Web hosting and open source
author: fl
created: 2025-03-17 10:46:16
intro: The complicated relation between open source and web hosting from our point of view
lead: This is not about WordPress founder Matt, who is angry about the web hosting service WP-Engine. It's a much smaller story, it's ours.
draft: false
figure:
  text: In real open source, you have the right to control your own destiny. -Linus Torvalds
tag:
  - opinion
  - changelog
---

## Our story

We started our PHP hosting business around 2012. Composer was just released. PHP 7 on the horizon. We aimed to create a hosting service for modern PHP websites and web applications.

The young Laravel community helped us getting started. Back then, I did not realized, how crucial and fragile this initial support by the community and those early adaptors was. Blinded by my ego, I thought that our great talent and superior service was the reason for initial success. It did not even crossed my mind to invest in a partnership with Laravel, I took all that for granted.

In 2014 Taylor Otwell (Laravel) launched Forge, a hosting service for the Laravel community. This was a big blow for our business, killing our stable inbound channel over night.

Luckily only half of our customers where using PHP frameworks to create web applications. The other half was classical websites usually done in a CMS. We where not interested in hosting WordPress.

So we invested to get some visibility with the young Craft CMS scene. With modern paradigms Craft CMS matched our platform quite well too. We really digged it. This time we invested to have a formal partnership with it's creators (Pixel & Tonic). We became recommended hosting partners, which in return would result in a steady stream of signups.

Eventually, Pixel & Tonic ended our partnership as they prepared to launch their own Craft Cloud hosting service. Another blow for us, not only business wise but also emotional.

## Open source software and hosting

> A lot of people who work on open-source software don't mind making money elsewhere. They aren't anticommercial. -Jimmy Wales

Open source projects require funding. Entrepreneurship can be an effective model. A related business can provide the foundation for the independent development of the OSS project. From a business perspective, the popularity of an OSS project can generate the leads. For website or web application software, a hosting solution is an ideal match, as it is a service that users of the software will need anyway. They will be happy to support their open source heroes.

Vercel is another hosting service with a tight open source software connection. The popular Next.js (React) framework comes from Vercel. Nuxt, the Vue based alternative has Nuxt Studio, an add-on service for Nuxt content.

The french PaaS Platform.sh is very close to Symfony project. The Symfony founder Fabien Potencier now works for them.

Laravel Cloud launched recently. That's another hosting business from Laravel Inc to monetize their reach. From my perspective the Laravel eco system is closing down making it even harder for us and others to be seen as an alternative.

## Our strategy

We don't have the resources to invest heavily in OSS. We lack time, financial resources, energy, and a viable idea to build our own OSS business vehicle. Our focus is solely on providing a web hosting solution. We aim to create a good product - [new platform in the making](https://new.fortrabbit.com). We can thrive with a tiny market share.

We bet on the long tail of a vivid PHP community with many open source frameworks and content management systems. We shamelessly use OSS trademarks to advertise our services, demonstrating that our platform is a good match and that we know a bit about running such software.

## In closing

Let's revisit the WP-Engine / WordPress controversy. Initially, I sympathized with the idea of a greedy web hosting company profiting from WordPress without giving back. Automattic, Matt's company, made $710M in revenue, while WP-Engine made $400M in 2024. It seems Matt is not the lone open source maintainer in need of support. I can't judge how much WP-Engine has contributed or should have contributed.

Our cost structure is very different from traditional hosting providers. We have [high infrastructure costs](/infra-research-2024), almost no marketing budget, while most of our energy goes into product development. Our ability to contribute back to OSS is very limited.

We use a lot of open source software to run our business, our clients are using a lot of open source software to interact with our services too. We couldn't do without. Some of those open source projects are already well funded. But there are others projects that can benefit from funding. Open source maintenance can be stressful, lonely and financially unrewarding. Where possible, we plan to sponsor open source projects more. We also aim to contribute to write well researched feature requests or issues.
