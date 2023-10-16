---
author: fl
created: 2015-05-18
published: true
title: I love assets
excerpt: CSS, JS and Images, how to generate and to deploy.
image: i-love-assets.png
tags:
  - webdev
---

## The why, what and how of automated static asset pipelines

We are currently working on a [big platform update](/roadmap-to-hack-app). For this, we plan to drop one of our core features: the locally attached network storage. That means that future Apps will not have persistent storage any more, we call them "ephemeral Apps". This new architecture will be faster and even more stable.

That also means that those 12-factor flavored Apps will not have the convenient SSH/SFTP access any more and you'll only deploy using Git.

But not all parts of your App are supposed to be part of Git: Runtime data like log files and user uploads and also **compiled static assets** such CSS/JS & images live outside Git. Further on i would like to explore opportunities to generate and deploy those fixed static files. Let's have a look back first:

## A look back: Legacy CSS/JS workflows

I think I first saw compressed JavaScript with jQuery. I learned about YUI compressor, but back then it looked like big guys tech to me. The JS and CSS I was writing where exactly the files that got delivered to the client. Remember [web standards](http://www.webstandards.org/), XHTML 1.0 Strict? Things where clean and easy.

That changed when I began working with CSS preprocessors. I suddenly needed a workflow to separate the authoring files from the one used in production. So i found the tooling to automate those build-processes and even help to do more. Things became "ugly".

## Why to pipeline

The benefits of using automated build processes are obvious:

1. make your life easier with better authoring tools
2. speed up page delivery with optimized files

## What to pipeline

Everything is possible. The most common tasks are:

**Compiling CSS preprocessors**: You enjoy authoring your CSS in less, Sass or Stylus. So you also need to convert this to plain CSS for production at some point.

**Compiling to JS**: You are writing your JavaScript in a language that compiles to JS, like CoffeeScript, TypeScript or Dart. So you'll also need to compile this to plain JS for production.

**Concating**: You multiple single JS or CSS files in authoring, but you don't want to have that many different calls for external files in production, so in the building pipeline you join them together to one big file.  

**Image optimizing**: You can make your vector- and raster-images even small than your graphic editors "save for web" export — use gifsicle, jpegtran, optipng, svgmin and pngquant.

**Minifying**: Get rid of all the characters that are only necessary to keep your files readable for humans. Remove all those white-spaces, and line-breaks, redundant declarations: compress it, uglify it.

**Gzipping**: Now turn your one line of uglified code into mojibake to make even smaller.

(**Deploying**: Get all the stuff up.)

## How to pipeline

That's what you want to have done, but which technology stack to use?

### Local JS task runner

TLDR; That's the popular choice these days, just use Gulp.

Why not use front-end technologies when dealing with front-end files? Task runners like [Gulp](http://gulpjs.com/) and [Grunt](http://gruntjs.com/) are a popular choice to automate your development tasks. They are based on Node.js, but they work side by side with whatever kind of language you are coding in.

### Your framework

Some frameworks have built-in asset solutions. These probably better fit into your workflow and come with additional features like: File versioning (for cache-invalidation), Dev/Stage scenarios, link-rewriting, deployment helpers …

#### Ruby on Rails

Let's remember: [SASS](http://sass-lang.com) was one of the first CSS-preprocessors. It's written in Ruby. In addition [Compass](http://compass-style.org/) is probably the first generation of micro-mixin-framework. Rails itself handles CSS/JS automation with [The Asset Pipeline](http://guides.rubyonrails.org/asset_pipeline.html).

#### Symfony

<!-- Ich weiss nicht, ob das so richtig ist?  -->

Symfony has a new (2015-04) [Asset component](http://symfony.com/blog/new-in-symfony-2-7-the-new-asset-component) as well as workflows to integrate [Assetic](https://github.com/kriswallsmith/assetic) with Symfony and Twig.

There is movement! @WouterJ just recently added an article to the Symfony Docs on how to [use Bower alongside with Symfony](https://github.com/symfony/symfony-docs/pull/5159), followed by a proposal for a new article on a [pure PHP asset solution](https://github.com/symfony/symfony-docs/pull/5166).

#### Laravel

Laravel has a clever approach by just integrating predefined Gulp tasks. It even has a fancy name: [Elixr](http://laravel.com/docs/5.0/elixir).

#### Other frameworks

You get the point. Mature frameworks have this built in. Play has [the Assets controller](https://www.playframework.com/documentation/2.0/Assets), Django [deals with it](https://docs.djangoproject.com/en/1.8/howto/static-files/).

### GUIs

DesignerDevelopers (like me) might consider stand-alone Apps with "click interfaces". I found [CodeKit](https://incident57.com/codekit/) useful to get started, other alternatives are [Koala](http://koala-app.com/) (free, cross-OS), [Crunch](http://crunchapp.net/) and [PrePos](https://prepros.io/).

## How to deploy

Now you have automated workflows to generate optimized versions each time you save your original JS/SASS file. How do you deal with it? Do you just put it in Git and deploy with the rest along, or do you define yet another asset pipeline task to deploy it.

### Static assets VS Git

Source control was designed to deal with code changes in your original authoring source files. It's actually not the place to put your ugly files in. If you just put your assets in Git you'll have to deal with bad side effects like:

1. **No diffing**: Compiled static assets are binary, they consist of one line, impossible and not and even necessary to diff.
2. **Merge conflicts**:  You'll run into conflicts when everyone in your team has "different" versions of compiled files.
3. **Bloating**: Your `.git` directory get's bigger and that makes everything slowers.

**Shame on us!** We are supporting you in such bad practices with "Git push to deploy". It's what everybody loves as it is such a convenient way to upload code changes. The only problem: it's a hack. Now what can we do about it?

#### 1. Put assets in Git, work around quirks

You can at least make yourself more comfortable by dealing with some of the quirks. Andrew Ray [describes in his blog](http://blog.andrewray.me/dealing-with-compiled-files-in-git/) how to: 

* Exclude built files from diffing in `.gitattributes`,
* don't let compiled files conflict in a rebase with a merge driver in `.git/config`, 
* rebuild files automatically with a Git hook. 

Other solutions to use branches or submodules for this.

#### 2. Put assets in Git Large File Storage

That's just an idea that came up while researching this topic. After [git-fat](https://github.com/jedbrown/git-fat) and [git-annex](http://git-annex.branchable.com/) [git-lfs](https://git-lfs.github.com/) is a new approach to actually deal with large binary files, but hey why not use it for something like this. Git Large File Storage needs to be installed on both, the client and the remote server to work.

#### 3. Exclude from Git, generate static assets on remote

In general we assume that you are compiling your assets in your local development environment. One can also consider to have the same setup on remote so, that you everything can be compiled on remote after a (Git) deployment (or even live on each user request) again.

I don't think that this makes much sense, as it is probably hard to debug errors for instance when your local dependencies differ from the remote ones.

#### 4. Exclude from Git, deploy separately 

Exclude your static assets from Git at all. Deploy them in a different way, maybe even to a different space such as a cloud object storage space. That means you have two deployments (with a platform like ours) — Git push and the "other one". The "other one" might be some rsync or some upload to an [external object storage provider](http://help.fortrabbit.com/external-services#toc-cloud-storage). The "other one" might be triggered with Git Hook.

That is probably the most professional and most complicated way. We do so with our web properties here — all JS, CSS and images are served from S3. This way you can also easily hook up a CDN for those assets. Serving those files from another domain improves performance (non-blocking).

Now, with our upcoming 12-factorish App you can't SSH in any more, so you'll probably need some kind of external space. 

A separate cloud storage might also help you with your runtime data.

> That’s dogma over practicality.

**[John Albin Wilkins](https://www.drupal.org/node/1821780#comment-6661544)** in a Drupal Community comment 


## Conclusion

Yes, asset pipelining with task runners makes sense. The automation of mundane tasks not only helped us to increase productivity; the file optimizations reduced page load time significantly. 

Now it only seems to us, that there are a thousand ways to do it. We are designing our service around deployment and hosting. So it's crucial that we get this right. What's your opinion and what's your practice? We are curious if you are considering solution 4 where you separate assets from Git deployment. Are you using this in practice, which cloud storage provider are you using? If using AWS S3, do you make use of IAM?

We are considering to implement a new "cloud storage" (working title) component, which basically makes using AWS S3 much more convenient, integrated tightly into fortrabbit. 

The upcoming [Amazon Elastic File System](http://aws.amazon.com/efs/) also looks promising. It could be a replacement for the persistent solution we currently have, although we are skeptical as we there are always two sides, NFS and Operating System. But for sure we'll keep an eye on that.