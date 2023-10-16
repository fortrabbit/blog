---
author: uk
published: true
image: 10-php-pillars.png
title: 10 pillars of modern PHP development
excerpt: Our best practices in PHP application design
created: 2015-06-04
tag:
  - webdev
---


## PHP development then and now

For most of us PHP developers writing applications now compared to ten or so years ago is quite a different endeavor. Back then, many of us were rather web designers; responsible not only for backend development, but database engineering, system administration, frontend programming and maybe conceiving and designing the very UI as well.

This has changed in recent years. Classical web sites are becoming more and more the domain of specialized SaaS - why write another blog engine, cooperate homepage CMS or small time ecommerce system if there are already so many available for (nearly) free? Or to put it the other way around: everything which can be easily automated (CMS, blog, ..) will be eventually. What cannot needs to be custom made.

So web developers changed themselves by specializing and concentrating on what cannot be automated so easily: web applications. Along with this came a new mindset on how PHP development should be done and what tools should be used.

# 10 pillars of modern PHP development

We often receive requests on how to design applications for our [hosting infrastructure](http://www.fortrabbit.com). While there are a thousand different use-cases, many deserving of a different approach, the following is based on our experience and should be viewed as a guideline.

Many people are using modern full stack frameworks, such as [Laravel 5](http://laravel.com/), [CakePHP 3](http://cakephp.org/), [Symfony 2](https://symfony.com/) or the like. Those already come with a set of style guides, patterns and recommendations.

However much is still up to the developer so here are our two cents on how a current PHP application development should be approached.

## 1. Code

The most important part of your application.

### Management

The code should be under version control. We go a step further and strongly recommend Git due to it's wide spread and availability across the board (and because we are not aware of truly superior alternatives). 

### Style

Adhering to [defined coding standards](http://www.phptherightway.com/#code_style_guide) will pay out: consistent code is [better comprehendable](http://www.cs.loyola.edu/~binkley/papers/tr-loy110720.pdf) by other members of a team and thereby adding new members is easier. No matter the size of the team (even for single developers): code maintenance can easily take up the [majority of a projects time](http://www.sersc.org/journals/IJSEIA/vol7_no5_2013/36.pdf) (thus money) and well formatted and documented code is the [primary factor](http://stackoverflow.com/a/1325617) in reducing those efforts.

Also it's just plain satisfying to read good code.

### Open sourcing

Open sourcing your application code (or at least modularized parts of it) can be an extremely good idea: free hands to harden the code quality, free marketing for yourself or your company and supporting the community as a whole.

Again, we'd like to put an emphasis on Git. Using an exotic revision control it could be hard to find developers which are willing to spare the extra time.

The before mentioned style will also impact the level of acceptance and willingness to participate: using existing standards helps allows newcomers to jump right in without wasting time on deciphering your intentions.

## 2. Tests

Automated testing has long been the black sheep of the PHP family. However, this has greatly changed; the legend it would double development time is nearly rooted out and it's now (luckily and) virtually unthinkable to contribute anything to most open source projects without a corresponding test.

A thoroughly [tested application](http://en.wikipedia.org/wiki/Software_testing#Testing_levels) brings a lot of advantages. My personal top three:

* Tested software can be far easier refactored
* Unit testing enforces modular design (increased re-usability)
* Tests provide a documentation and example code

There are lots of [benefits](http://en.wikipedia.org/wiki/Unit_testing#Benefits) but in the end for me it boils down to this: Better code — less headache.

## 3. Dependencies

Dependencies should (of course) be handled with [Composer](https://getcomposer.org). Since the code is strongly coupled with specific package/library the dependency declaration (`composer.lock`) should be in the version control as well (in my opinion).

The actual package/library files (`vendor` folder) should not be part of version control, since their revisions are already handled by the declaration, which is thereby under version control and it would be redundant to do both.

### Modularization

Being a user of libraries/packages also changes your mindset (or at least positively re-enforces it) towards modularization of your own code. This in turn leads to less code repetition across projects and thereby reduces effort and increases quality in the long term. And let's not forget the ability to open source those modules, as mentioned above.

## 4. Configuration

Configuration, if badly used, can be a great hindrance when migrating your application. More so, it can be a security risk.

### Separate config from code

Using the environment is definitely the best choice. By this we primarily mean (operating system) environment variables but we think local configuration files (or a combination thereof) are a valid choice as well - as long as their deployment is clearly defined.

The best rule of thumb to measure whether the configuration is cleanly separated from the code we heard is: Could you open source your code without exposing any credentials right now? If the answer is Yes, then you are good.

**Bad**: in some `config.inc.php`:

```php
$database = "foobar";
$user     = "foobar";
$password = "foobar";
```

**Good**: Environment variables from Apache `SetEnv` or the like:

```php
// $_SERVER["DB_NAME"];
// $_SERVER["DB_USER"];
// $_SERVER["DB_PASSWORD"];
```

### Complex config
Environment variables can contain complex information (think: multi level array). It should be marshaled as JSON and encoded into base 64 so it is easily modifiable and readable from outside the application.

```php
// somewhere in the bootstrap, assuming all encoded variables are prefixed with "::"..
foreach ($_SERVER as $k => $v) {
    if (0 === strpos($v, "::")) {
        $_SERVER[$k] = json_decode(base64_decode(substr($v, 2)));
    }
}
```

## 5. Assets

Asset data, such as (compiled) CSS, Javascript, images and so on, are truly hard to decide upon. In short - and with limitations - my recommendation is to keep them under version control.

At length: Compilation of CSS and Javascript or creating modified instances of images requires a surprisingly large and diverse tool set which comes with a large dependency set of their own (think c compiler for node extension which shrinks images using image magick bindings vs complete Java runtime for some CSS compilers vs ..). This increases the complexity of the deployment infrastructure unnecessarily. Then there is the responsibility problem: Assets are often handled by the frontend developers of the team. As all specialized developers, they have their tools which work great for them. Forcing asset compilation in the release cycle means they need to limit themselves to the tools available here.

For a truly in-depth discussion about this topic please see [Frank's previous article](/i-love-assets).

## 6. Runtime data

Runtime data includes all file based data (i.e. no databases), which is generated at runtime by user interaction (eg file uploads) or as an result thereof (eg multiple instances of an image). Classically this is handled using a local or network attached file system (see also [flysystem](https://github.com/thephpleague/flysystem)).

We recommend cloud storages (such as [S3](http://aws.amazon.com/s3/), [Cloud Files](http://www.rackspace.com/cloud/files), [Cloud Storage](https://cloud.google.com/storage/docs/overview), ..), since they: inherently solve various scalability issues (scaling application out over multiple servers or geographical regions), prevent future migration headaches (data lock-in), natively balance load by separating execution (PHP scripts) and delivery (static files).

## 7. Resources

Resources are all services which are used by the application, such as databases, caches, queues, the afore mentioned storages, mail delivery providers and all that.

### Abstraction

Access to resources should be abstracted. The degree of abstraction should depend on probability (eg if you are planing to scale out then you'd use an adapter for a local resource, which later will be replaced by an adapter for a network capable resource) and feasibility (eg a cache abstraction is almost always simple, while an abstraction allowing to substitute a MySQL database with, say, ElasticSearch much more effort, eg using the [repository pattern](http://code.tutsplus.com/tutorials/the-repository-design-pattern--net-35804), and this effort must be justifiable).

The location of resources must be substitutable by configuration (as described above).

**Bad**:

```php
$conn = new mysqli($servername, $username, $password);
```

The code will be tightly coupled to MySQL databases with a specific driver. If either MySQL databases or this driver is not available in a new environment the code must be refactored.

**Good**:

```php
use Illuminate\Database\Capsule\Manager;
// $_SERVER['DATABASE'] = ["host" => "localhost", ...]
$mgr = new Manager->addConnection($_SERVER['DATABASE']);
```

Using a different SQL database can easily be achieved. Using a different MySQL database location can be easily configured.

### Weak coupling

All "soft" services, without which the application still can run (eg a database driven application could not run without the database) should be disengageable easily. Say a mail service is used to greet new users with a welcome mail: make sure you can switch it off with with a single command, in case the mail provider temporarily goes down. Even better: automate that. Best: Use a queue which can back-off and retry by itself.

## 8. Deployment

In a web application project, there are few things more feared, more disaster prone and hence over and over delayed than big upgrades into production. [Deploy early and deploy often](http://programmer.97things.oreilly.com/wiki/index.php/Deploy_Early_and_Often) circumvents this by continuous integration of small upgrades. The primary requirement to allow this is a simple, transparent and fast deployment.

We are huge fans of Git based deployment, since it already comes with a history and allows easy integration of build scripts. However, application needs and environments differ greatly, so the perfect deployment for all situations is probably not to find.

Good code quality, testing and good measured abstraction pay out in the long run, having a easy to use deployment workflow is essential for the day in, day out work.

## 9. Stages

While automated testing provides a good foundation, when code meets content there is still lot's of room for mishaps. Hence there is the concept of staging. Having a (working) local setup of the application already provides the first stage: the *development stage* (or *local stage*). The other stage, which always exists, is of course the *production stage*: the live web application. Now there is lot's of space in between for testing, review and whatnot.

In general, all stages should try to approximate the production environment as closely as possible. The more they deviate, the less sense they make.

How many stages should be used depends on project size, team size, team setup, kind of application and so on. Please read a [more comprehensive discussion here](/multi-stage-deployment-for-website-development). As a general rule of thumb we recommend three stages: A local development stage, of course the production stage and a testing stage in the same environment as production (of course: separated).

## 10. Scalability

You probably have heard that you are now a [DevOp](http://en.wikipedia.org/wiki/DevOps). This means: when writing your application, you must be aware of the underlying infrastructure so you don't fight with it's weaknesses, but rather leverage it's strength.

It's a bit of a side effect of the cloud infrastructure. Before: all you had to do (and often could do) was vertically scaling your machine: bigger server. So you would not care as much where the bottle neck was, since there was only one solution. Now that you can not only scale out (horizontally), but do that for every resource individually, you should know which one slows you down. Or what you can do in terms of application design to compensate for that. Or especially: which new resource you can attach to boost the performance.

In short: You got access to the red button and with great power comes great responsibility.


## Summary

**It's harder now**: You must know more about coding patterns, deployment strategies, testing and application design than ever before. **It's easier now:** a fleet of new tools, better services and coding standards help and support as never before.

> The art of writing PHP code has changed. A lot. And we think it's now more interesting than ever.


## Further readings

When writing about modern application development in the cloud, one must mention the [12-factor App](http://12factor.net/) by Adam Wiggins. It lays out the complete design and life-cycle of a modern application. 

<!--
Please read the full document linked above. In short it asks and answers the following:

1. How code is managed (version controlled)
1. How dependencies are managed (isolated from system)
1. How configuration is handled (in the environment)
1. How resources (eg databases) are to be attached (easily substitutable)
1. How the release cycle works (separated stages)
1. How statelessness is leveraged (self-contained processes)
1. How encapsulation using containers is to be done (only defined ports exposed)
1. How horizontal scalability is integral (results from statelessness)
1. How resilience is to be approached ([crash-only](http://en.wikipedia.org/wiki/Crash-only_software) design)
1. How the development setup should look like (development, staging, production)
1. How health and insights are to be monitored (post evaluated log stream)
1. How administrative tasks are to be done (console)
-->

Corey McMahon wrote up a great three part series on how to apply (as close as possible) the 12-factor draft [here](http://slashnode.com/the-12-factor-php-app-part-1/).

From a pure PHP point of view, I can subscribe to the abstract ideas, but not to (all) of their concrete approaches. In addition, I think the scope of their document overreaches what should be the concern of a developer.

