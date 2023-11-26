---
author: fl
published: true
created: 2017-08-03
title: "Market overview: CDN services"
excerpt: An opinionated field guide on developer-friendly CDN services.
lead: We evangelize the idea of decoupled hosting. This post gives you an overview about cool content delivery services.
image: cdn-overview-poster.gif
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'HTTP/2, SPDY, webp, CDN, gzip, http, cache-control, expires, pragma, ssl, DDOS protection, Content Delivery Network, Highwinds, Limelight, Bitgravity, bluemix, cachefly, brotli, WCO, Web content optimization, CDNIFY, RTT, HEIF'
---

## A generation of CDNs for developers

Not so long ago, Content Delivery Networks was only for the enterprise only. Now, there are more offers for developers and medium projects — with pay-as-you-go pricing and additional features. As a web developer you have an overwhelming choice of services. This post helps you through the jungle to find the best performance and security optimization tool for your needs.

### When to use a CDN

CDN is cool tech to play with. But mind that for many websites and applications it might be overkill. Keep your tech stack simple. Additional features come at the cost of additional complexity (like cache invalidation) and additional points of failure. CDN benefits are:

* Increased speed: especially for distant visitors
* Optimization: by offloading (less CPU, traffic & storage) and better delivery

Rule of thumb: Consider a CDN when you have a few thousand requests per hour and you are serving a lot of static assets. The most common use case is to serve images.

### How a CDN works

The basic idea is this: Websites are global, visitors are local. Content is delivered faster, when served from a server closer to the visitor. The more points of presence, the closer, the better. So the visitor should get the heavy (static) assets — mostly images, but also JS, CSS, fonts and maybe even cached versions of full pages — from a nearby server. That reduces latency and round-trips (RTT). And that also helps with performance as it offloads requests from the application web server.

### How implement it

So you do something like this …

```html
<!-- No CDN: image loaded from a relative path from the server -->
<img src="/img/cheshire-cat.jpg">

<!-- With CDN: image hotlinked -->
<img src="//myaccount.mycdn.com/img/cheshire-cat.jpg">
```

… and the CDN will distribute the Cheshire Cat to multiple locations around the world.

#### Push & Pull

You might ask yourself, when and how are these images uploaded to the CDN?

Classical CDN are working as **push CDN**s, so it's actually your responsibility to upload the assets to the CDN. The benefit is that you have a good control about your media.

All the cool kids are using **pull CDN**s (reverse proxying). Why? Because it adds on top: The images are uploaded locally and then pulled to the CDN "automagically". Please see our extended [post about HTTP caching](https://blog.fortrabbit.com/mastering-http-caching) & how to implement a pull CDN. TLDR: You'll easily find plug-ins for your CMS and example configs for your framework.

### Additional services

CDN functionality is only one part of performance and security. Often also included with a hosted service:

* Image optimization
* Image conversion to webp
* Cache header optimization
* Cache purging (when you have changed a file)
* DDOS protection
* Web Application Firewall
* GZIP (& brotli) compression
* JS & CSS file bundling
* CSS & JS minifying & concating
* HTTP/2 delivery
* TLS (SSL, https)
* Statistics
* Video streaming
* (Static hosting)
* API
* …

All this correctly combined can really help to fasten up things. But don't forget: clean code is the best base for a fast website. Keep your stuff slim (also see our [application design guide](https://help.fortrabbit.com/app-design-pro)) and avoid the [website obesity](http://idlewords.com/talks/website_obesity.htm). And of course you know: Decreasing page load time can increase conversions, sales and even SEO.

## CDN providers

We are using [keycdn](https://www.keycdn.com/) from Switzerland, which is popular among devs. Other developer-friendly CDN providers are [fastly](https://www.fastly.com/) and [cdn77](https://www.cdn77.com/). MaxCDN and Highwinds recently joined [StackPath](https://www.stackpath.com/). IaaS users might have a look at [Cloudfront (AWS)](https://aws.amazon.com/cloudfront/), [Azure CDN](https://azure.microsoft.com/en-us/services/cdn/) or even [Google Cloud CDN](https://cloud.google.com/cdn/). Enterprise clients might have look at [Akamai](https://www.akamai.com/), the [enterprise CDN by IBM](http://www-03.ibm.com/software/products/en/enterprise-content-delivery-network-ecdn) or [GlobalDots](http://www.globaldots.com/).

**[cdncomparison.com](http://cdncomparison.com/)** by betahex is an almost up-to-date table of CDN providers with all features.

### Special mention

#### CloudFlare

[CloudFlare](https://www.cloudflare.com) is the popular choice. It is a suite of services with a lot of "magic". It's plug and play: You point (DNS) your domain to CloudFlare and that's it. ClouFlare got a bit of bad rep when [some HTTPS pages where found in the Google cache](https://news.ycombinator.com/item?id=13718752). It has a free plan for personal use and of course a WordPress plugin. I personally like to have some more control about certain aspects, so I haven't used it yet.

#### greta.io

[greta.io](https://greta.io/) is a (new) startup aiming to "revolutionize" data distribution — even with P2P (?!). They have a "headless" setup to integrate the service with just a little javascript — totally free and without the need of an account. A unique feature is that images are "lazy loaded". I have integrated the service here on our blog. Check out the [post list page](/) - it will load the images when you scroll down. Inspect it in your browser dev tools to see what's going on.

![Lazy loading images](/dist/img/cdn-scrolling-lazy-load.gif)

<small>Above: greta lazy loading in action.</small>

### Image processing and CDN services

As mentioned: In most cases, those images (of cats) are making your website heavy. So I like to include image delivery services under this topic as well. In fact, they usually come with an integrated CDN + all the magic you want for your images.

Image transformation (crunching image uploads for web delivery) can be outsourced to free up CPU power. ImageMagick — for instance — can be resource-hungry and it usually runs on the web facing server, so your visitors might have to wait a little longer while crunching is in progress.

Imagine an URL-API for image sizes like `/img/w_400,h_400/cat.jpg`, so there is no need to define thumbnail and preview sizes upfront. You can change that with the design. Responsive images are easier to setup as well. Less work for your framework or CMS, more magic in the background.

[Cloudinary](http://cloudinary.com/) and [imgix](https://www.imgix.com) are the biggest providers in this space, followed by: [Transloadit](https://transloadit.com/), [libpixel](https://libpixel.com/), [Filestack](https://www.filestack.com/), [Blitline](https://blitline.com/). New services: [rokka](https://rokka.io/en/) by Liip(!?) from Switzerland and [Sirv](https://sirv.com).

## Final words

Commercial CDN services are doing a useful job. YOU the sophisticated web developer should be aware of this.

## Disclosure

We have no business relation with any of the above mentioned providers. These are not affiliate links. Everything here is 100% opinionated and subject to changes and errors.
