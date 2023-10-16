---
author: fl
created: 2016-01-06
title: E-commerce in 2016
published: true
excerpt: What's going on in e-commerce?
lead: We are constantly on the lookout for new software. This is a brief look on current developments in the e-commerce section.
image: shoppingcart-2970468736_0fdb725f9f_o.jpg
tag:
  - opinion
---


Online retail business is growing. People buy more stuff online. And all of this is occupied by Amazon. Well, not entirely… One small village of indomitable Gauls still holds out against the invador. You, the developers and entrepreneurs building a custom e-shop, are a Gaul.

DICLAIMER: There are as many types of e-commerce as stars in the sky. This article is a look at those blinking lights from below with focus on new trends, lightweight and cloud-ready systems. We have a PHP background, which is the language of many E-commerce systems. And we come from Germany which is also home of many projects.

<!--

e-commerce, ecommers, eshop, esale, estore, eat it bot. online shopping

-->

## Categories & trends

Some ecommerce solutions are specialized for certain product categories, digital goods, physical products, tickets, coupons, mobile commerce, comparison shopping, all kind of things. Some are made for certain markets and languages. Here are some notable distinguishing features:

### Shopping cart software

We'll mostly cover "full e-commerce solutions" for serious business here. To quickly sell some swag from your website you can use a "**shopping cart system**". Those webshops usually come with less features and are easy to use and easy to plug in to any site.

### E-commerce as an CMS Add-On

Some eshops are integrated as **add-ons for established CMS**. The Drupal space is mostly ruled by [Drupal Commerce](https://drupalcommerce.org/); for WordPress we have: [WooCommerce](https://www.woothemes.com/woocommerce/), [WordPress eCommerce](https://wpecommerce.org/), [MarketPress](https://marketpress.com/), [Cart66](http://cart66.com/) and many many more as you can guess.

### E-commerce & frameworks

Modern PHP frameworks are based on Composer. You'll find some commerce components on packagist, mostly for specific tasks (payment, billing, cart-solutions …). The **[Sonata project](https://www.sonata-project.org/)** is a set of bundles based on Symfony2. [Lavender](https://github.com/lavender/lavender) (not much going on) is an e-commerce framework built on top of Laravel. [Aimeos](https://aimeos.org/) provides ecommerce bundles for Typo3, Typo3 Flow, Symfony2 and Laravel.

### Hosted e-commerce

Most online stores shown here are classical self-hosted e-commerce systems — these are of course more interesting for us as a hosting provider. But of course there are: **Hosted e-commerce solutions** — Commerce as a Service (CaaS). For example: [Shopify](https://www.shopify.com/), [Bigcommerce](https://www.bigcommerce.com/), [Volusion](http://www.volusion.com/), [Big Cartel](https://www.bigcartel.com/), [3dcart](http://www.3dcart.com/), [Kong](https://trykong.com/), [Squarespace commerce](http://www.squarespace.com/commerce/). Some hosted ecommerce solutions are made for micro-businesses (shopping carts) — where "no coding skills are required". But they are not limited to that: Shopify for instance has it's own template language: Liquid which gives you much freedom about the frontend.

### E-commerce by API

**API is the new black**: Salvo Zappalà outlined concepts for API driven e-sales in his post about [building next-gen ecommerce](https://medium.com/@salvoadriano/building-the-next-generation-ecommerce-26093f98d2d7) — imagining the e-commerce system as the "back-end" as part of an Service Oriented Architecture. Front-ends are a web client, mobile apps and an admin panel. That also blurs the boundaries between programming languages.

The Drupal Commerce Guys are going in that direction, Sylius and Sellvana as well. And there are already some startups out there. Those are mostly closed source and hosted:

* [Schema.io](https://schema.io/) API first and only
* [Moltin](https://moltin.com/) hosted + API
* [Mozu](https://www.mozu.com/) hosted + API, brainchild from Volusion, US
* [commercetools](http://www.commercetools.com/) (ex sphere.io) from DE, Berlin

### Licensing

You can have a professional e-commerce system for literary free. Or you can pay LOT'S of money for a license. This can even happen to be for the same software. And it all makes sense. E-commerce is undeniable a space where money is involved, nobody creates an e-commerce software to make the world a better place.

That doesn't mean that all software is closed source. You can find interesting open source business models here as well: additions costs extra, commercial support, professional license + community edition …

## Rookie e-commerce software

We are mostly interested in those newcomers here of course. Composer packages are making it easier to develop ecommerce solution as a lot of basic stuff is already been taking care of. So naturally there is a new generation of e-commerce:

**[Craft commerce](https://craftcommerce.com/)** has a brother: Craft is a PHP CMS system with a good reputation. The maintainers Pixel & Tonic have recently released version 2.5, along with the new Craft commerce — an e-commerce solution based on Craft. It looks quite modern. A license currently costs $999.

**[Sylius](http://sylius.org/)** from Paweł Jędrzejewski (Poland) is still under development and looks promising. ~2k GitHub stars

**[Sellvana](https://www.sellvana.com/)** is an upcoming ecommerce solution by [unirgy](https://twitter.com/unirgy) and others. 5 GitHub stars

**[Elcodi](http://elcodi.io/)** Symfony components, Composer — keep talking. This is Elcodi from Barcelona, another young promising candidate. ~390 GitHub stars

**[Thelia](http://thelia.net/)** (still in version 2) from France is an ecommerce based on Symfony2 components with Smarty 3 templating engine.  ~550 GitHub stars

**[Mothership](http://mothership.ec/)** is another newcomer that promises to combine e-commerce with a point of sale (ePOS) solution. ~15 GitHub stars

**[Arastta](https://arastta.org/)** (from the comments below) is yet another newcomer. The core team behind it is Miwisoft which comes from Istanbul. Ararstta is based on Symfony components and also follows the API approach. There is a free open source edition and a hosted one. Version 1.2.1. was released in December 2015. ~100 GitHub stars

**[Yo!Kart](http://www.yo-kart.com/)** (also comments) is rooted in India (I dig this). It's available as a hosted and a self-hosted version, it's not really open-source.

## Veteran e-commerce software

Old does not have to be rusty. It also means means tried and tested, feature complete and maybe even in a new version:

**[Magento](https://magento.com/)**, started in 2008, is the elePHPant in the room. Everything is covered: there is a community edition and a enterprise edition. It's a huge eco-system with modules (extensions), themes and an active community around it. Many digital agencies are specialized solely in Magento. The second major version was expected for 2011, but it took a bit longer. Magento 2.0 was finally released in December 2015. ~3k GitHub stars

**[Prestashop](https://www.prestashop.com/)** started in 2005, is from France and shall [soon](https://github.com/PrestaShop/PrestaShop/blob/develop/composer.json) be based on Symfony components. ~1.5k GitHub stars

**[Shopware](https://en.shopware.com)** has been around since 2004 and is still [looking sexy](https://github.com/shopware/shopware/blob/5.1/composer.json). It was born in Schöppingen in Münsterland. There is a free community edition as well as professional and enterprise ones. ~350 GitHub stars

**[Spryker](https://spryker.com/)** is a high-end solution. Developed inhouse as "Alice & Bob" by Rocket Internet and later by Project A as "Yves & Zed". A license will cost at least €100K, but you won't find prices on the website.

**[Pimcore](https://www.pimcore.org/en/product/multi-channel-e-commerce-platform)** is also rooted in the enterprise sector and does it all. It's a CMS that has an integrated multi-channel e-commerce platform (Enterprise Add-On). ~500 GitHub stars

**[Reaction Commerce](https://reactioncommerce.com/)** is an open source Javascript (build on Meteor) for ecommerce, currently in beta. ~1.7k GitHub stars

**[Spreecommerce](https://spreecommerce.com/)** is probably the most notable e-commerce system written in Ruby. ~7k GitHub stars — But i learned (see below) that it is no longer maintained and succeeded by [Solidus](http://solidus.io/).

**[OXID Esales](https://www.oxid-esales.com/en/home.html)** is yet another bedrock from Germany.

### Even more

The list should goes on: [Lemonstand](https://lemonstand.com/), [osCommerce](https://www.oscommerce.com/), [OpenCart](http://www.opencart.com/) (don't use it, [pushad claimed](https://www.reddit.com/r/PHP/comments/2tu3x5/whats_the_best_php_ecommerce_platform_to_get_into/co2f3ow)), [Avactis](http://www.avactis.com/), [loadedcommerce](http://www.loadedcommerce.com/), [zeuscart](http://zeuscart.com/). A special mention for the most-old-school-looking website goes to [AFCommerce](http://www.AFCommerce.com/). On AngelList you can find [24431 e-commerce startups](https://angel.co/e-commerce).

---

## Finding the best e-commerce software

As you might guess: There is no one single best solution. It all depends on your needs and preferred flavor. Find the right mix of customization, **community**, usability, theming, extensibility, hosting-performance, scalability, costs, support, localization features and security yourself.

The new solutions are, well: new — sexy, lightweight, developer-friendly, and maybe not as feature rich and hardened. The old solutions are, well, old — monolithic, full-blown, slow, lame, but functional after all.

### An opinionated word on hosting

If you are planning to start an ecommerce project based on PHP, check out our platform here, it's fast, reliable and we really care about PHP.

<p class="dimmed">
    Image credit: For the illustration I made use of Multi Cart Pile-Up photo by Gayle Nicholson via <a href='https://www.flickr.com/photos/gayle_n/2970468736/in/photolist-5wuqSd-9o64sn-6erszG-d97eEy-8r1e6z-oBXzi8-4jAV4j-2hti5r-mu9xyR-33GbDA-CTVe4-hBKXeg-2hxHxJ-jHdSKu-zUZXdw-nKCgno-nkT8VY-3dnGq-dqJGNk-f4tB4-7xk7Yi-k2Wnzw-2htiG2-3dnDW-rtcfG7-q8gdn3-3dnFj-3dnCn-ghxtU3-3dnAT-nFR6xY-boiadE-7xmtV1-4ci5bY-ccQDM-nzsu6Y-3S5P-ASM7aM-6tj5y-9FGmjR-qCfnaP-bPMzPH-hbXWft-mdNc5g-4QZBqu-7ACCK6-4rDFEx-e87Y24-7AeHUM-66tHbf'>Flickr</a>
</p>
