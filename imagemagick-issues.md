---
title: ImageMagick issues
created: 2019-03-04
published: true
author: fl
excerpt: The backstory of recent issues related to image transformations.
lead: During the last week we have had some trouble with ImageMagick. Sorry for the inconvenience. This article provides some background about what happened.
keywords: imagick
image: imagemagick-issues-poster.gif
tag:
  - chronicles
---

## ImageMagick on fortrabbit

As you know: [ImageMagick](https://www.imagemagick.org/) is a very well known image transformation library which has been around for ages. It lives as a ready-to-run binary in many operating systems. It helps you to transform images, like from one size to another (big > thumb) or from one format to another (PNG > JPG).

For PHP there is an additionally interface, called "imagick" which is installed as an extension and exposes a programmable interface for ImageMagick in PHP. The combination of these two in PHP is so popular, you could call it a standard of the LAMP stack.

You will most likely have been using ImageMagick for years. Whenever PHP does an image transformation, like when thumbnails are created, it is probably doing all the magic in the background with ImageMagick. The GD Graphics Library is an alternative also available here.


### A design trade-off

Our Apps are designed as lightweight containers serving fast PHP processes. Allocated resources are limited. Image transformation on the other hand are resource hungry by nature. Loading images in memory (uncompressed) requires a lot of RAM and processing and compressing them with ever advancing codecs will keep even the most modern CPU busy. You can try it at home: Transform images with any program and watch your CPU spike.

From our point of view, in an ideal web application architecture, such operations should not be mixed with anything that happens on the frontend. Image transforms should not make any user wait. With the Professional Apps we offer [Workers](https://help.fortrabbit.com/workers) to outsource such resource hungry tasks into the background. But setting this up requires extra efforts, which might be overkill for a standard website.

So we aim to bring a good solution for Universal Apps - a balance between performance and expected results. We therefore have been limiting ImageMagick memory usage with a "policy.xml" file for quite a while already. The limits are designed to give each ImageMagick process a reasonable limit while still performing as expected. With Universal Apps, each ImageMagick process was limited to 64 MB of memory. This setup has worked great for years.


### Recent imagemagick updates

We recently updated ImageMagick from version 6 to version 7. One of the goals was to bring "**webp**" support 😎. It now seems to us, that something changed with the new ImageMagick version.


### Hard to detect issues

We rolled out the update around a month ago (10th of Feb) and we initially did not see any issues, neither in our tests we did before nor in production after the update. But one by one, more and more image transformation related issues appeared. So we tried to find a connection between them. 

![](/dist/img/imagemagick-corrupted-image-1.jpg)

![](/dist/img/imagemagick-corrupted-image-2.jpg)

Sometimes, but not always, great abstract art like the examples above was produced. Source: footage from clients.

We finally found out, that image transformations done on larger images coming in (>3000px each side) and relatively large images going out (>600px each side) tend to lead to errors. Those error cases either have been generating the grey images or we simply saw hanging processes and 5xxx errors with no images at all in the end.

Only a small number of clients were affected by these issues, but for some of them issues were critical.


## The current situation

We have investigated all kinds of settings. We now think to have found a solution. It offers much better use case coverage in the ImageMagick policies. A [patch](https://status.fortrabbit.com/incidents/ysbw39h49n1s) has been applied globally just recently.

Now, Apps are getting the maximum available memory for ImageMagick. If your Apps runs on a bigger plan, it gets more memory for ImageMagick. The default also increases from 64 MB to 128 MB. We also increased the swap size that ImageMagick itself can use.

Those two settings together (RAM & swap) have provided much better results in our testing. We are carefully watching results now. The patch is not perfect, we still see few cases, with very large images that will still fail. More memory (bigger plan) or smaller source images can also help.

We are still investigating this and are looking for ways to further improve the service further.


<h2 id="further-actions">Further actions</h2>

To get rid of past failed transformations, your action might be required.

Image transformation are usually cached on disk. Those caches now - after the incident was going on for almost a week - can contain corrupt files. Image transformations are often only generated the first time a user calls a page containing images. Generated images are then cached on the local file system and will be available without any computing from there on. Now, there might be corrupted files on disk with your App already. So if you still have issues with image transformations, please make sure to clear the caches first, so that the images can be re-generated.

How to delete image caches depends on the framework or CMS in use, maybe settings and even plugins.

The actual cache files are kinda temporary runtime data, so they are usually not stored with Git. 

In most cases, the caching is a combination of files on disk and entries in the database. The CMS / framework needs to keep track of cached files. So there likely gonna be methods available. Simply deleting files might not solve the issue. 

Pro Apps don't have persistent storage. So the transformed images, when configured correctly will end up on the Object Storage. There might be local copies on the ephemeral file system as well. The local copies will be deleted with each deploy. Again, usually you just have to use the available methods. With Universal Apps, the generated images usually will end up on the file system of the App.

### Craft CMS

Craft CMS users have three ways to trigger a rebuild to delete already cached broken images:

1. **Control Panel**: You can do so in the Craft Panel (on fortrabbit) under "Utilities" > "Clear Caches" > Check "Asset transform index". Make sure that the flag "allowAdminChanges" in "general.php" for the fortrabbit environment is set to "true" (default is false here), otherwise those options are not accessible.
2. **Craft CLI (3.0.37+)**: Login via SSH and issue `php craft clear-caches/transform-indexes`
3. **MYSQL**: Delete specific rows in "assettransformindex" or truncate the whole table.


### Laravel

Laravel does not have image transformation capabilities on it's own by design. Libraries are often used. The most popular one is [Laravel Medialibrary](https://docs.spatie.be/laravel-medialibrary/v7/introduction). Please see the docs of what you have in use.

### WordPress

WordPress of it's own does not seem to bring any methods to deal with image caches. There is a dedicated plugin called "[Regenerate Thumbnails](https://wordpress.org/plugins/regenerate-thumbnails/)". But all popular cache plugins, like "W3 Total Cache" and "WP Super Cache", have options to clear image caches builtin.

- - -

Sorry for the inconvenience this have caused on your side, one more time! Contact us if you still have trouble, we are here to help.