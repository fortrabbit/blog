---
title: imageMagick patch 2
excerpt: Some smaller internal improvements mostly on imageMagick ahead.
created: 2019-08-16
author: fl
lead: We are currently preparing for a smaller platform update. Mainly, this is about releasing a new patch, improving imageMagick performance - general stability and security improvements included.
figure:
  src: imagemagick-issues-poster-2.gif
tag:
  - changelog
---

## Run down and timing

The updates will affect all Apps (Uni and Pro). There is no - or just a very short (>1 minute) - expected downtime for web delivery. We will run the updates sequentially, App after App. Pro Apps on production plans are planned to have near-to-zero downtime. For the deployment services (Git, SSH and SFTP) we do not expect service interruption.

Please keep an eye on our [status page](https://status.fortrabbit.com) where we are going to post intermediate updates. TIP: You can also subscribe there.

We are going to run those updates **Tuesday, 20th of August 2019**  first in US and a few hours later in EU. The total expected maintenance window is 4 hours for each region.

* **US maintenance** — 08:00 UTC + 4 hours window
* **EU maintenance** — 13:00 UTC + 4 hours window

## Addressing imageMagick performance

We have once again optimized our imageMagick (the open source library squeezing your jpgs) distribution for more speedy image transformations. We are looking forward that this will make transformations faster, especially for image-heavy websites.

### Backstory

Back in February we ran a major upgrade on imageMagick - from version 6 to version 7 — most prominently now featuring `webp` support. But, some serious performance degradations followed. They have been addressed with a quick follow up patch — see our [blog on initial imageMagick issues](/imagemagick-issues). Back then we adjusted the `policy.xml` to better make use of available memory. The situation got much better, but some Apps where still suffering.

![](/dist/img/imagemagick-corrupted-image-2.jpg)

Broken images like the one pictured above and/or frozen websites —  504 time out errors  — when image transformations where ongoing here and there.

### Learnings with our clients

We have had hard times identifying common patterns on the issues. They were happening under different circumstances and setups. But we are very fortunate to have such great clients! **Thank you!** Detailed and excellent bug reports and even test pages where provided. We learned a lot together.

### Image size matters

Digital photo cameras are getting better and better over time. So the source images are having higher resolution nowadays. Mobile phones have 16 MBP and professional cameras up to 45 MBP. With our testing we found that the input size always matters, as the full image needs to be read in memory, even to produce the tiniest thumbnail. But the target output size, also seems to matter. The worst transformation case is a lot of huge image that need to be transformed into big images.

### Craft CMS in focus

While there have been some cases with WordPress, most often we dealt with Craft CMS installations. We learned that Craft 2 was more affected than Craft 3 and probably that an older PHP version (7.1) also has a negative impact.

#### Craft CMS queueing

The current implementation of the **Craft CMS web job queue** can break your website and can also play a negative role in this context. Oliver developed the [Craft Async Queue plugin](https://github.com/ostark/craft-async-queue) to address this. We recommend to use it in any way — with or without many images. It often helps to make better use of available resources. Andrew Welch just blogged about [robust queue job handling in Craft CMS](https://nystudio107.com/blog/robust-queue-job-handling-in-craft-cms) — have a look.

In our optimal hosting design thinking, the actual image transformations should not be done form the frontend PHP processes anyways. They should be outsourced to something like a Worker. Another alternative might be to outsource image transformations and delivery to an image hosting service such as IMGIX,  Cloudinary and alike.

### GD as an alternative

As a mitigation we often suggested to use "GD library" instead imageMagick. Most modern CMS and frameworks are supporting both anyways. It can easily be switched with a few clicks in our Dashboard. When only transforming JPGs the output quality might not be as good, but usually with less memory consumption and possibly smaller JPGs — it is still a considerable good alternative. It should be noted, that it will also choke, when the images provided are too big, but usually with a meaningful error about exceeded memory instead of just eating up all memory and blocking all processes.

## Blackfire fix for Craft CMS

While trying to debug those performance bottlenecks in [Blackfire](https://blackfire.io) we found another issues: Blackfire does not report well in combination with Craft CMS and Twig. Template names did not showed up correctly. Something like `__TwigTemplate_5b91f909…::doDisplay()` was shown.

We reported that as a bug and it was patched with the Blackfire extension version 1.27 which (hopefully) will also be included with the coming updates, so that we — and everyone using Blackfire in combination with Craft CMS — will finally get something more readable like this: `_partials/footer-nav.twig::doDisplay()`.

## The new imageMagick patch

Last not least — we are now deploying a newly compiled version of imageMagick, optimized for faster transformations, with the following changes:

* **HDRI is disabled.** We believe that High Dynamic-Range Images are not needed in this context of delivering general images swiftly.
* **Q8 only.** Support for 16bit depth images is disabled. We believe all standard web image formats today are usually using 8bit anyways.

The test results are pleasing: better performance through using much less memory — up to 75% reduction in RAM usage — while keeping the same quality. We will carefully monitor the roll out in production now.

### Cleaning broken images

Your framework/CMS does not know if an image shows a cat or just grey lines. Broken jpg files need to be removed and the image transformations need to be re-run. Here is a brut-force way to remove all image transforms for Craft CMS (for Universal Apps) on the local file system:

```bash
# 1. Login via ssh to the App
# 2. remove transformed images from file like so:
$ rm web/assets/*/_*/*.*
# 3. clear caches 
$ php craft clear-caches/transform-indexes
```

Next time someones visits the website, all image transforms will be re-run (first unlucky user). The first run will take some seconds — depending on the number of images and size per page, but it will be faster than before and less error-prone. From the second visit on the images are cached on the server side anyways.

## Other client facing changes

Alongside with under the hood updates, some new client facing minor patch versions will be installed as well. Here is the (hopefully) complete list:

### Changed PHP versions

* PHP73 (7.3.5) >  7.3.8 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_3)
* PHP72 (7.2.14) > 7.2.21 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_2)
* PHP71 (7.1.29) > 7.1.31 - [changelog](https://www.php.net/ChangeLog-7.php#PHP_7_1) < Support until end of year only!

### Updated extensions

* mongodb (1.5.3) > 1.5.5 - [changelog](https://pecl.php.net/package-changelog.php?package=mongodb)
* phalcon (3.4.3) > 3.4.4 - [release notes](https://github.com/phalcon/cphalcon/releases/tag/v3.4.4)
* blackfire php probe (1.25.0) > 1.27.0 (see above)
* blackfire agent (1.26.0) > 1.27.3 - [changelog](https://packages.blackfire.io/binaries/blackfire-agent/1.27.3/CHANGELOG)
* `convert` **ImageMagick** (7.0.8-46) > 7.0.8-60 - [changelog](https://imagemagick.org/script/changelog.php)
* `mysql` (5.7.26) > 5.7.27
