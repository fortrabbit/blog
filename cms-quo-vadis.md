---
title: CMS, quo vadis?
author: os
published: true
excerpt: Are content management systems ready for the cloud?
figure:
  src: cms-frameworks-drawing.jpg
created: 2015-10-09
tag:
  - opinion
---

# Are content management systems ready for the cloud?

I follow general discussions about PHP in podcasts, on Twitter, on [Reddit](http://www.reddit.com/r/php) and on sites like [phpdeveloper](http://phpdeveloper.org/) or [phptoday](https://www.phptoday.org/) a lot. And I wonder **why content management systems are not a topic these days?** It seems like that they don't exit anymore. People talk about PSRs, APIs, design patterns, Composer packages and frameworks.

Most of our clients are building applications from scratch, usually on top of a framework like Symfony, Laravel, Slim or Phalcon. [Our Twitter stream](https://twitter.com/fortrabbit) is dominated by these topics as well.

Let me backtrack a little first: Before we started fortrabbit we ran a digital agency for about 8 years. We did jobs for small and large clients. We touched many technologies to manage content in the web: from plain PHP to CakePHP, Magento, Drupal, Fatwire (Java) and last not least WordPress of course. I was wondering what have changed. So, I did some research to update myself.

Surprisingly most of the CMS projects still exist. They evolved, some more, some less. And there are even many newcomers out there. Here is a short overview of my (superficial) investigations:

## Established CMS platforms

Most of the large <abbr title="free and open-source software">FOSS</abbr> projects exist over a decade now and have matured over time. They have created their own developer communities and their own (isolated) ecosystems of plugins or modules to extend the core functionalities. Specialized agencies or consultants with deep knowledge are usually required to build websites on top of these platforms.

To stay relevant almost every established big platform releases a new major version every 3-4 years. Currently it's not so much about new features. There is a movement towards [interoperability and standard compliance](http://www.php-fig.org/) now.

### Drupal

Drupal is problably the most popular CMS in the US, however the founder Dries Buytaert is from Belgium. When I worked with Drupal for the first time version 7 was in beta. Multilingual support was a project requirement. It turned out that 6 modules were required to translate all bits and pieces. Additionally the whole architecture with render arrays and hook functions felt weird to me — I wrote OOPish code before.

Now, about 5 years later, Drupal 8 is in beta/RC and [moves quickly towards stable](https://drupalreleasedate.com/) - this time with i18n support in core. But more importantly it feels like a modern PHP application. There is less proprietary stuff to learn, when you've worked with Symfony components like HttpKernel, Twig or Routing before.

Drupal 8 is still a complex beast, but there are tons of educational resources out there. Another plus is the huge community of developers with a decent level of knowledge. Chances are high someone else had a similar problem before and *There is a Module for That*™.

### eZ Publish / eZ Platform

For a long time eZ mainly targeted the publishing industry. This was reflected in the name of the core product: eZ Publish. In 2015 they changed the focus by introducing [eZ Platform (free) and eZ Studio (commercial)](http://ez.no/Blog/What-Releases-to-Expect-from-eZ-in-2015). Both software products use the same kernel, based on Symfony Framework 2.7/3.0 and [other libaries](https://github.com/ezsystems/ezplatform/blob/master/composer.json) like flysystem, doctrine/dbal and stash.

"Alpha4" of eZ Platform (aka eZ Publish 6.x) was released some days ago, so it might take some time until it becomes production-ready. But the current stable version (5.4) already looks quite modern and is officially [supported until 2017](https://support.ez.no/Public/Service-Life).

### Typo3 / Neos

Typo3 is/was the first choice for many European web agencies. For many years it was the <abbr title="open-source software">OSS</abbr> defacto standard solution for German government and NGO websites. My personal experience with Typo3 is very limited. The latest version of Typo3 CMS (7.5) looks quite modern: It [requires PHP 5.5 or later](https://git.typo3.org/Packages/TYPO3.CMS.git/blob/HEAD:/INSTALL.md), integrates with Composer and has a proper file system abstraction layer.

But there are also Flow and Neos. Backed by the TYPO3 Association, Robert Lemke and Karsten Dambekalns started a complete rewrite known as Typo3 Neos (based on the flow framework) around 2008. Both branches are co-existing under the Typo3 umbrella for years and are actively maintained. This led to confusion for newcomers.

However, recently with the 2.0 release, Neos (without the Typo3 prefix) is run independently. It seems to me that this move frees a lot of energy in the community. Neos 2.0 and Flow 3.0 (< this is the version number) aim to be ready for the cloud and try to [liberate from the Typo3 legacy](https://www.neos.io/news/infrastructure-for-our-community.html).

### SilverStripe

SilverStripe is the PHP CMS with the biggest popularity in New Zealand and Australia. [A new major version (4)](http://www.silverstripe.org/blog/sneak-peek-silverstripe-4/) is on the way. SilverStripe 4 should be better integrated within the PHP ecosystem: by leveraging other 3rd party libraries like flysystem or Swift Mailer, but also by decoupling there own underlying framework and splitting it into reusable packages. SilverStripe 4 is expected to be released in 2016.

For the current version (3.1 / 3.2 beta) I found two modules to support S3 file storage: [silverstripe-cloudassets](https://github.com/markguinn/silverstripe-cloudassets) and [silverstripe-s3cdn](https://github.com/silverstripe-australia/silverstripe-s3cdn).

To my surprise [Christopher Pitt](https://twitter.com/assertchris) moved to New Zealand and joined the team earlier this year. To me this is a good sign hiring a forward thinking member of the PHP community and I hope this will drive forward the cultural change in the SilverStripe community.

### pimcore

The first time I heard of pimcore was at the local [Berlin user group](http://www.bephpug.de/slides.html) in 2012. Christoph Luehr introduced is as the CMS he uses [at work](https://basilicom.de). During my research I've installed the latest version (3.0.6) and tried to configure the system. But I was stuck at some point - probably not pimcore's fault - complexity lies in the nature of "enterprise software".

**Me:** pimcore is build on top of ZF1. Can we expect a change towards ZF3 in the future?

**Bernhard Rusch, CTO / Co-Founder of pimcore:** We will replace many components we've build inhouse and ZF1 components as well with modern libaries. This means pimcore will not be tightly coupled to a specific framework anymore. Instead we'll use mature libraries from different vendors - this process will happen step by step.

Bernhard Rusch mentioned as well that the next major version is expected for mid 2016. A early pre-release was [annouced last month](https://www.pimcore.org/en/resources/blog/pimcore+4+beta+announcing+the+first+public+pre-release+of+the+open-source+enterprise+suite+for+pim%2c+cms%2c+dam+%26+commerce._b13633).

### WordPress

According to W3Techs Usage statistics: WordPress powers 24% of the internet — an [impressive number](http://w3techs.com/technologies/overview/content_management/all). It means that Wordpress is one important factor for the huge market share of PHP. At the same time it is responsible for the bad reputation of PHP (we have lamented about that before).

The minimal required PHP version is still 5.2, that version was released 9 years ago and is unsupported for almost 5 years. Modern language feature like namespaces, traits and anonymous functions are not availiable in PHP 5.2 - and that's how the core looks like.

The strategy of small iterations might be a good thing, but it also keeps a lot of legacy in the code. Matt Mullenwegs [keynote talk at WordCamp Europe 2015](http://wordpress.tv/2015/07/04/matt-mullenweg-keynote-qanda-wordcamp-europe-2015/) gives you are good picture about it.

Despite all the criticism one have to admit that only some tweaks and [plugins are required](http://de.wordpress.org/plugins/search.php?q=s3) to run Wordpress in the cloud already.

## CMS Newcomers

The newcomers are less bloated and not as "feature complete" as their bigger brothers. They aim to solve smaller problems with simpler solutions. This approach works good for small to medium sized websites, marketing campaigns or for clients with smaller budgets to just edit some pages.

### Pagekit

There was some buzz about [Pagekit](http://www.pagekit.com/), when the folks at [YOOtheme](https://yootheme.com/) (the company behind Pagekit) launched the first public alpha in July 2014 — 2 years of development behind closed doors.

During the last months the initial wave of excitement turn into silence. But then, some weeks ago, the [first beta appeared](https://pagekit.com/blog/2015/09/10/pagekit-beta-released) - a complete rewrite, with new a Vue.js based user interface and a CLI for scaffolding. Things may change until the 1.0.0 release and there are still some important features missing — like custom fields, multi-language and cloud storage support. Nevertheless, it is a project you should keep an eye on.

### Bolt CMS

Bolt 2.0 was released about 10 months ago - the main code contributions come from [Two Kings, a dutch agency,](http://www.twokings.nl) who founded the CMS in 2012. During the last months an increasing number of people are using Bolt and are contributing to the project as well.

As I had no experience with Bolt, I gave it a try. There are to ways to install it: 1) composer create-project, 2) .zip file download (for shared (FTP) hosting). I've tried both, the Composer way feels much better to me. The Composer based skeleton is basically a `/public` folder with a `index.php` file and some static assets, and a `/app` folder where config and cache lives. All other dependencies, including Bolt itself, are in the `/vendor` folder.

The bootstrapping and the configuration is pretty straight forward - there is not much new stuff to learn if you've worked with Silex and the Symfony Config Component before. The configuration is .yml based, environment specific configs are possible and for edge cases you can overwrite settings on the fly in PHP.  

Filesystem abstraction is advertised with the 2.0 release, [but it's not fully implemented](https://github.com/bolt/bolt/issues/4095) - the only available adapter is the LocalAdapter. It would be really nice to see alternatives like S3 as an configurable option, or at least an [extension](https://extensions.bolt.cm/).

### Craft CMS

Craft differentiates in two ways: First: except for the Twig template engine, Craft CMS is not built on top of Symfony components. The underlying framework they use is Yii. And second: itˋs not free open source. You can try all aspects during development, a limited personal edition is free as well, but for commercial usage a (small) one time license fee is required. This way the maintainers assure further development and bugfixes.

The company behind Craft is called Pixel & Tonic, a dev shop from US with experience in consulting and <abbr title="Expression Engine">EE</abbr> extension development. They started their own software about two years ago. Craft is quite popular in the (US) EE scene, but largely unknown in Europe. However, some of our clients from the UK use it and are very happy with it.

I've installed [the developer preview](http://buildwithcraft.com/3) of the upcoming version. The configuration was a no-brainer. By default it supports multiple environments based on the domain it runs on, but it was fairly easy to detect the environment by ENV variables (a common practice these days). I haven't tried to upload media assets, but under the hood it works with our good friend [flysystem](http://flysystem.thephpleague.com/).

The next major release (Craft 3) adopts PHP language features like traits, namespaces and late static bindings. And everything feels quite modern, except the lack of using Composer. But that might change in the future.

### All the others

Further more I have also checked out: Joomla! (veteran), asgard CMS (L5.1), october CMS (L5.0), Grav (flat file), Fork CMS, PyroCMS (3.0, L5.1), sulu CMS — but enough for now.

## Is your CMS ready for horizontal scaling?

Running a content management system "in the cloud" requires not much effort these days — since most modern CMS are prepared for that case.

An important aspect of cloud hosting is that multiple copies of your code spread across multiple machines - known as horizontal scaling.

The main difference to a single VPS you must be aware of: The only thing which lives in the web-servers file system is your code. You can not rely on the local file system to avoid inconsistent session states. Sessions must be stored centralized, in an external database — think Redis or Memcached. The same applies to the application cache. And finally, all user uploads must be offloaded to a central place - AWS S3 or Rackspace Cloud Files are a good choice for storing and delivering images, music or any kind of static assets.

If you roll your own cloud setup at AWS, Rackspace or Digital Ocean you must implement some kind of load balancing, a centralized logging and a way to [distribute your code](http://help.fortrabbit.com/deployment-architecture-video). Erika Heidi did a [good introduction](https://www.digitalocean.com/company/blog/horizontally-scaling-php-applications/) on that. You should read it to understand the benefits and implications of horizontal scaling.

With managed cloud platforms like Heroku, Google App Engine, Microsoft Azure and fortrabbit as well, you don't have to care about the whole infrastructure layer.

## Final thoughts

Back then, I preferred to build custom back-ends on top of frameworks, instead of using a CMS to manage dynamic website content. This approach wasn't very efficient, but it was owed by the fact that the editor experience of open source content management systems was really bad. To enable editors managing content on their own, intensive trainings were required. Fortunately this changed, user experience becomes more and more important.  

For agencies and developers, 2015 is the right time having a closer look at the new solutions out there. There is no single best CMS. Instead, each product has a mix of strengths and weaknesses that are derived from its underlying architecture or market position.

My suggestion: Invest a decent amount of time to evaluate software you may use for the next 5-10 years. Don't trust feature lists and the marketing! Choosing a CMS is crucial business decision: It's about technology, concepts, maintainability, predictability, the developer community and not least about attracting future employees and clients.

## Bonus

And here is a video of me painting the logos:

<div class="responsive-video">
    <iframe src="https://www.youtube.com/embed/_IenQ-uPxwo" frameborder="0" allowfullscreen></iframe>
</div>
