---
author: fl
created: 2021-04-14
published: true
title: Image processing services intro
excerpt: A field guide on image transformation and optimization providers
lead: Learn about image processing service providers here. What are they? What problem do they solve? What options and alternatives are available?
image: cute-cat-pic.jpg
imagecredit: Cute cat pic by Tracie Hall via <a href="https://www.flickr.com/photos/twobears2/37604436396/in/photolist-6Pjxge-6PoG69-6PjxfH-3eqRoo-ZnmzJx-v8waGk-ZhYyPE-ouKa9x-8ojtiF-YYuFpw-YYuF1q-Ym1g6M-8mi4pJ-4FQTyx-9BAaQK-6ko4xj-9BD67S-9BA7ek-9BD52w-8S2zXo-9agUQR-8guKEj-8S9bLE-9BA6ee-8KYihX-7fztGU-99iUFr-6Pjxer-66qMJP-achUUZ-5r9CxN-nmb3b-9FBcjV-5syW5Y-5bbX9P-741cFi-5NKLao-5BYhxD-8vPXAz-8zzshp-qqguz-aF5ZXH-7CpNdc-2eyi4Ti-7k1BhP-7k1ATp-7k1B5T-9NeM1U-7hmoNZ">Flickr</a>
tags:
  - opinion
---


## Scope and disclaimer

This is a quick overview about image processing services. This is not a deep comparison or a step by step integration guide. The author has only little or no first hand experience with the services themselves. There is no business association.

## What is image hosting as a service?

An image processing service is a convenient collection of tools to easily deliver images for your website. It usually consists of a Content Delivery Network (edge caching) and an image transformation engine (image resizing on the fly). It fits nicely in a micro service oriented architecture. There is often also an easy to use API accessible by passing URL parameters. Consider requesting a thumbnail version of an image like this: `image.jpg?height=400&width=400&mode=crop`.

## What problem does image hosting solve?

### Faster websites

Images are often the biggest byte chunks of websites. That's why you want your images to be as small as possible and to be delivered in sizes relevant to specific visitors. Also you want the images to be served from a location that is close to the visitor.

### Better hosting resource usage

Your hosting service has limits. Here at fortrabbit, our Apps are designed for fast web delivery processes. When you upload photos to a CMS, these images need to be processed to multiple formats:

+ A thumbnail and a large version
+ Multiple sizes for devices with different resolutions
+ Multiple image formats for different browser engines, webp and jpg

So one uploaded original image might result in 20 images files for web delivery. Here is a simple example HTML markup for a full-sized image that can be served in 4 different sizes and two formats (webp and jpg):

```html
<picture>
  <source 
    type="image/webp" 
    srcset="
      cute-cat-pic-2700x1209.webp 2700w, 
      cute-cat-pic-1800x806.webp 1800w, 
      cute-cat-pic-900x900.webp 900w, 
      cute-cat-pic-600x600.webp 600w" 
    sizes="100vw"
  />
  <source 
    srcset="
      cute-cat-pic-2700x1209.jpg 2700w, 
      cute-cat-pic-1800x806.jpg 1800w, 
      cute-cat-pic-900x900.jpg 900w, 
      cute-cat-pic-600x600.jpg 600w" 
    sizes="100vw"
  />
  <img 
    src="600x600/cute-cat-pic-600x600.jpg"
    alt="Cute cat pic" 
  />
</picture>
```

With standard web servers image crunching is usually done by open source tools like [ImageMagick](https://imagemagick.org/) or [GD](https://github.com/libgd/libgd). Image transformation is a CPU heavy task that can take some time (even seconds!) until executed and it can also use a lot of memory. Calling image libraries is wrapped in PHP on webhosting services like ours. That means a PHP process is occupied until an image has finished being converted. Good news is, once an image version is created, it can be stored on disk for later usage.

With suboptimal configuration (crazy eager loading, too many sizes) and/or wrong settings (no cache on disk) and/or extensive use (super large source images or many images) this can lead to serious web delivery problems or even end in 504 time-out errors.

In addition to standard image processing, additional tools (jpegoptim, optipng, pngquant, SVGO, gifsicle) to further optimize images are popular among performance-aware frontend developers these days. These tools often require a lot of processing power and are therefore not available here.


### How an image hosting provider works

Most image hosting services work as "origin pull CDNs" at their core. That means images are uploaded as usual with your CMS like so:

+ `yourdomain.com/uploads/newimage.jpg`

Then you configure the image hosting service to use that folder. In your templates instead of using a relative path on the domain of the website use an external link like this:

+ `user.imageprovider.com/uploads/newimage.jpg`

In addition you can set up a sub-domain so you don't have to use the domain of the image provider:

+ `cdn.yourdomain.com/uploads/newimage.jpg`

After that you can use URL parameters to grab a different versions:

+ `cdn.yourdomain.com/uploads/newimage.jpg?height=400`
+ `cdn.yourdomain.com/uploads/newimage.webp?height=400`

Additional flavours and features are available.

## Image hosting providers overview

Here is a list of some image optimization services:

+ [imgix.com](https://www.imgix.com)
+ [imagekit.io](https://imagekit.io)
+ [piio.co](https://piio.co)
+ [libpixel.com](https://www.libpixel.com)
+ [imageboss.me](https://imageboss.me)
+ [kraken.io](https://kraken.io)
+ [sirv.com](https://sirv.com)
+ [cloudinary.com](cloudinary.com)

There are client libraries for programming languages. There are also plugins for popular CMS's like WordPress, Craft CMS or Shopify and Magento to easily include the services. Some providers can also integrate with an AWS S3 bucket. Most will have HTTP/2 or even HTTP/3 support. Some might have AI/ML tools for intelligent cropping or automated tagging. Some also offer video encoding.

Comparing prices is a bit hard, since vendors use individual pricing models - most are usage based (pay as you grow).

## Alternatives

### CDN

While there are dedicated image processing services, the service offering can also blend with other services. Some CDN providers also provide image transformations services:

+ [developers.cloudflare.com/images](https://developers.cloudflare.com/images/)
+ [cloudinary.com](https://cloudinary.com/)
+ [bunny.net](https://bunny.net/)

That might be convenient since it gives you a one stop shop.

### Transform images on the web server

For normal usage you can still use your general purpose web server to do the job.

### Run your own

You can also host your own worldwide image transformation service. [Imaginary](https://github.com/h2non/imaginary) is open source software written in Go.

### Others

You can also tinker together something like this on your cloud infrastructure provider using serverless functions. On AWS there is some [Serverless Image Handler](https://aws.amazon.com/solutions/implementations/serverless-image-handler/) glue.


## My experience

Are image transformations services worth the money and the effort?  
It depends!

You should definitely look into this if you are running a successful e-commerce site. Sometimes using such a service can be an economic choice: pay some more for the image service while paying less for the web hosting itself.

I do a lot of client support for our hosting platform. I often get requests for advanced image optimization because people see a bad Lighthouse score or they have read some article like [Creating optimized images in Craft CMS](https://nystudio107.com/blog/creating-optimized-images-in-craft-cms). That's one of the reasons I wrote this blog post.

I would recommend first trying to take full advantage of the tools available before thinking about further optimization. Often the jpg compression level can be set to lower level when images are scaled down. Sometimes I see that images are not served in optimal sizes and resolutions. Sometimes I see other performance issues that might be fixed first.

My tip: Prioritize the areas of your website performance optimization. Go for the low hanging fruit first. Image sizes can play a major role. But before considering outsourcing image transformation, see what you can do with existing tooling and some creativity.
