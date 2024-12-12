---
title: Web hosting and open source
author: fl
created: 2024-12-12 14:45:19
intro: The complicated relation between open source and web hosting from our point of view
lead: This is not about Matt Mullenweg, WordPress/Automattic ($710M 2024 rev), who is angry about the web hosting service WP-Engine ($400M 2024 rev). It's a much smaller story, it's ours.
draft: true
figure:
  text: In real open source, you have the right to control your own destiny. -Linus Torvalds
tag:
  - opinion
---

## Our history

We started our PHP hosting business around 2012. Laravel was gaining ground. Composer was just released. PHP 7 on the horizon. We were pretty exited about all that PHP. So we aimed to create a hosting service for modern PHP websites and web applications.

We got our initial MVP released quickly. It was naive with a few fundamental flaws. Yet, it had git push to deploy and a deployment pipeline with Composer.

The young Laravel community helped us a lot getting started. Back then, I did not realized, how crucial and fragile this initial support by the community and those early adaptors was. I thought that our great talent and superior service was the reason for initial success. It did not even crossed my mind to invest in a partnership with Laravel.

Time passed and we have been busy to create a 2.0 version of the platform while and keeping the lights on. fortrabbit is bootstrapped. Back then, it was only us three founders. We are product people. We like to build stuff. We are not good at marketing.

In 2014 Taylor Otwell (Laravel) launched Forge, a hosting service for the Laravel community. This was a big blow for our business, killing our stable inbound channel over night.

We pivoted to get some visibility with the young Craft CMS scene. With modern paradigms Craft CMS matched our platform quite well. We really digged it. This time we invested to have a formal partnership with it's creators (Pixel & Tonic). We became recommended hosting partners, which in return would result in a steady stream of signups. Eventually, Pixel & Tonic ended our partnership as they prepared to launch their own Craft Cloud hosting service. Again quite a blow for us, not only business wise but also emotional. We like Craft CMS.

## Open source software and hosting businesses

> A lot of people who work on open-source software don't mind making money elsewhere. They aren't anticommercial. -Jimmy Wales

Open source projects require funding, entrepreneurship can be an effective model. A related business can provide the foundation for the independent development of the OSS project. From a business perspective, the popularity of an OSS project can generate the leads. For website or web application software, a hosting solution is an ideal match, as it is a service that users of the software will need anyway. They will be happy to support their heroes.

Vercel is another hosting service with a tight open source software connection. The popular Next.js framework comes from Vercel.

The french PaaS Platform.sh is very close to Symfony project. The Symfony founder Fabien Potencier now works for them.

## Our strategy

We don't have the resources to invest heavily in OSS. We lack time, energy, and a viable idea to build our own OSS business vehicle. Our focus is solely on providing a web hosting solution. We aim to create a great product ([new platform in the making](https://new.fortrabbit.com)) that works well and is fun for developers to use. We are not aiming for world domination, we can thrive with a tiny market share.

We shamelessly use OSS trademarks to advertise our services, demonstrating that our platform is a great match and that we know a bit about running such software.

## The other side

So far we have covered software to create websites and associated hosting business models.

We use a lot of open source software to run our business, our clients are using a lot of open source software to interact with our services too. We couldn't do without. Some of those open source projects are already well funded. But there are others projects that can benefit from funding. Open source maintenance can be stressful, lonely and financially unrewarding. Where possible, we aim to sponsor open source projects more. We also aim to contribute to write well researched feature requests or issues.
