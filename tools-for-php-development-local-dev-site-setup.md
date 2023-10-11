---

author:       js
created:      2020-07-30
publish:      published
title:        "Tools for PHP development — local dev site setup"
excerpt:      "What PHP development tools are available? What are the pros and cons of each tool?"
lead:         "The PHP ecosystem is diverse and has brought forth such industry heavyweights as WordPress, Drupal, and Laravel. Having a local PHP development environment set up allows one to develop and test sites and apps on one’s own machine. Without this, one needs to push any code changes to a remote staging environment for testing; a time-consuming and inefficient process."
image:        'local-php-dev-poster.gif'
imagecredit:  ''

---


Not only does a local PHP development environment **speed up and simplify development**, when done correctly it also allows different team members to use the same environment on their respective machines. This reduces the amount of friction between team members and allows for smoother deployments.

While the advantages of local PHP development are clear, the process of getting a dev site up and running **can be one of the least enjoyable parts of a PHP development** project. For WordPress, an integrated solution in the form of [Local by Flywheel](<https://localwp.com/features/>) exists. But for the generalized case of “PHP development” everybody seems to come up with their own solution.

There are **many ways to set up a local PHP development environment**, and developers and designers alike are looking for ways to streamline their local development. Our discussion of the topic will revolve around three central questions:

1. [**What does a local PHP development environment consist of?**](#php-development-environment)  
    What is a local PHP development environment?  
    What software components and settings are required?  

2. [**What should a local dev site setup look like?**](#local-dev-site-setup)  
    What considerations should we make?  
    What guidelines can we stick to?  

3. [**What tools are available to set up a local PHP dev site?**](#php-development-tools)  
    What are the pros and cons of each tool?  
    What tool is best suited for different use cases?  

## <a class="anchored" id="php-development-environment">What a local PHP development environment consist of</a>

In essence, a local development environment comprises **everything needed to *run* local dev sites**. This commonly includes software that needs to be installed and configured to work together in concert, such as a web server, database, and so forth.

Note that a development environment may be specific to a language or ecosystem. As such, a developer **may need to set up multiple development environments** on their machine. Each development environment, in turn, may be used to run multiple dev sites.

Let’s look at all of the parts a local development environment consists of:

1. **Software stack**

    For most PHP projects, this will include a database and web server, in addition to PHP itself and the underlying operating system. To give an example, the venerable LAMP stack consists of **L**inux + **A**pache + **M**ySQL + **P**HP.

2. **Project codebase**

    This is the custom code that our actual app or website consists of. The codebase will normally be held in a Git repository.

3. **Environment configuration**

    While the codebase should be the same for production and local environments, there are a number of settings that will differ between environments. These include database credentials, site URLs, ports, and the like.

    By convention, these settings are excluded from version control and are instead held in so-called `.env` files. In production, the use of `.env` files is often discouraged for performance reasons. In this case, the values are instead directly made available by the environment.

4. **Development tools, scripts, and configuration**

    For development, we will normally use a number of tools, such as Git, Composer, Node, Yarn, Gulp, and so forth. Some of these may only be needed for local development, others may also reside on the server.

    Additionally, we often end up writing custom “glue” code to tie things together. This includes shell scripts, Git hooks, as well as configuration files. Generally, these code files should be under version control, but may be in a separate repository.

5. **Local host name configuration**

    Whereas the preceding points pertain to both local and remote environments, this point and the following apply only to local development.

    When running dev sites locally, we need to provide a way of mapping local host names back to our sites. To give an example, when accessing a local dev URL such as `http://devsite.local` in the browser, how is this request passed on to the site we’re developing?

    The canonical way to set this up is to add custom entries in the `/etc/hosts` file. Alternatively, a tool such as DnsMasq may be used to automatically configure local host names for our projects.

6. **Virtualization / containerization tools + configuration**

    Virtualization / containerization is the method of choice for local development, and so we will need the appropriate software installed on our local machine. This includes tools such as Vagrant or Lando.

    These tools are normally controlled via a configuration file (Vagrantfile, Landofile, etc.), which should be under version control.

7. **Shared folders**

    When running a virtualized development environment, we often find the need to share files between our local machine and the virtual machine / container. For example, we can share our local project codebase to the virtualized environment. On our local machine, the codebase is just a bunch of files. But inside the virtualized environment, where we can run the code, our project comes alive.

    The standard way to accomplish this is to set up a network-shared folder. Everything inside this folder on the local machine will be accessible inside the virtualized environment.

As should be clear by now, a local development environment consists of quite a few interrelated parts. As such, there are many ways to set things up, with ample room for us to end up with suboptimal results. While development tools can help with some of the setup, the **precise balance of components is specific to each development workflow**. We therefore look for guidelines to find a good solution.

## <a class="anchored" id="local-dev-site-setup">What our local dev site setup should look like</a>

![local-php-dev--7515248418_831c15e4d7_o](/dist/img/local-php-dev--7515248418_831c15e4d7_o.jpg)

<small>Photo of an old Apple computer by Steve Jurvetson via <a href="https://www.flickr.com/photos/jurvetson/7515248418/">Flickr</a></small>

In essence, we want to be able to run multiple dev sites in parallel. Each dev site may require different dependencies and configuration. Ideally, we want to have a **standardized approach that we can rely on for every dev site** we want to set up.

Here are some guidelines for the sort of system we want to end up with:

1. Set up a dedicated local development environment. This means we’re able to **run our web-based software and access its services on our own machine**.

    Without this, we would need to push code to the server to test any code changes. Not being able to test code locally seriously slows down development. Furthermore, if we need to push before testing we’ll likely also end up polluting our repository with superfluous commits in the process.

2. **Isolate the development environment** from our physical machine’s operating system.

    We want to protect our system from becoming corrupted when updating or adding a dev site. Likewise, we need to protect our existing dev sites from becoming corrupted when changing our system.

3. **Isolate each dev site**.

    We want to avoid version conflicts and interference between dev sites. Adding a new site should not break existing sites; updating dependencies for one dev site should not cause a version conflict in another one.

4. **Ensure ability to deploy to production and staging**.

    We need to be able to push code and configuration from our local development environment to the remote environments. How to set this up depends, but generally there will be some form of Git deployment. Keep in mind that some files will likely be outside of version control. For those, we may need to employ custom sync scripts.

5. **Keep the local development environment as close to the production environment** as possible.

    We need to be able to match the dependencies and services in the production environment to our local development environment. This also means we need to be able to adjust the locally installed software when changes to the server are made.

6. Make sure we **know how to recreate our dev sites**.

    On one hand, this is crucial in the case of a catastrophic failure. On the other hand, whenever we need to onboard a new team member it’s nice to be able to get them set up without hassles.

## Four general ways to set up a local dev site

In principle, all four ways can be used to run local dev sites. However, in practice **most use cases are best served using a virtual machine- or container-based approach**.

1. **Set up all of the stack components on our local machine:**

    Examples: **Custom LAMP-stack**, **Valet**

    ✓ Highest possible performance of any solution  
    ⨉ No isolation of dev environment and local machine  
    ⨉ No code-based configuration layer  
    ⨉ Lack of dev site isolation

2. **Use a pre-packaged stack with GUI:**

    Examples: **XAMPP** / **MAMP** / **WAMP**

    ✓ Easy setup  
    ✓ GUI  
    ⨉ No code-based configuration layer  
    ⨉ Lack of dev site isolation

3. **Install all the stack components inside a virtual machine (VM):**

    Examples: **Vagrant**, **Homestead**

    ✓ Comfortable  
    ✓ Powerful  
    ✓ Dev site isolation via separate virtual machines  
    ⨉ Resource-hungry  
    ⨉ Lots of disk space needed for dev site isolation

4. **Distribute the stack components across multiple containers**:

    Examples: **Docker**, **Lando**, **DDEV**

    ✓ High performance  
    ✓ Low disk space requirement per site  
    ✓ Dev site isolation  
    ⨉ Performance issues if not running Linux  
    ⨉ Known issues with certain tools and techniques

## <a class="anchored" id="php-development-tools">Tools for running a local PHP dev site</a>

We’ll look at the pros and cons of each tool. Be aware that **some of these tools cannot be used in parallel.**

1. [**Vagrant**](#vagrant) (VM)
2. [**Homestead**](#homestead) (VM)
3. [**Valet**](#valet) (System)
4. [**Docker**](#docker) (Container)
5. [**DDEV**](#ddev) (Container)
6. [**Lando**](#lando) (Container)

### <a class="anchored" id="vagrant">Vagrant</a>

![local-php-dev--vagrant](/dist/img/local-php-dev--vagrant.gif)

Vagrant is a popular tool for **configuring and running a local development environment inside a virtual machine**. To accomplish this, Vagrant works with different virtual machine providers, such as VirtualBox, VMware, etc. To set up the development environment, Vagrant uses a provisioning tool, with Chef and Puppet being major examples.

To tie everything together, Vagrant employs a Ruby script called a “Vagrantfile”. In theory, the **Vagrantfile contains all of the information needed to replicate a dev environment** from a given box. However, in practice one may end up with a minimal Vagrantfile and the actual configuration pushed off to the provisioning tool’s configuration.

Development with Vagrant starts with a “box”, which is a pre-packaged environment geared towards a specific use case. There are **many [publicly available boxes](<http://www.vagrantbox.es/>) to choose from**; these can range from a bare Linux / Unix operating system to a fully-configured dev environment. For PHP development, one can choose from a range of specialized boxes. These commonly include pre-installed software such as:

- Apache and / or Nginx
- MySQL or MariaDB
- PHP 7.x
- PHP-fpm
- Git
- Composer
- Xdebug

Besides the software components, a box normally comes with **network interfaces and ports set up** and ready for use. This should allow one to get started, although some tinkering may be required to get everything configured for the specific use case.

Fortunately, Vagrant makes the **process of configuring the development environment easy**: configuration is stored in simple text files, which should be held under version control. After a change to the configuration is made, one re-provisions the machine. Should something go wrong in the process, it is straightforward to tear down the machine and start over.

Configuring a **Vagrant box affords a lot of control**. However, for most PHP development use cases it’s probably a better idea to start with Homestead.


Website: [vagrantup.com](https://www.vagrantup.com/)  
Supported operating systems: Linux, macOS, Windows

### <a class="anchored" id="homestead">Laravel Homestead</a>

![local-php-dev--homestead](/dist/img/local-php-dev--homestead.gif)

Homestead is a **Vagrant box provided by the Laravel project**. The contents of the box are geared towards PHP development:

> “Laravel Homestead is an official, pre-packaged Vagrant box that provides you a wonderful development environment without requiring you to install PHP, a web server, and any other server software on your local machine. No more worrying about messing up your operating system!”

Homestead comes packed with lots of cool features: one can run multiple dev sites inside a single Homestead machine, each with its own PHP version and SSL setup. There are **dedicated commands for common operations** such backing up and restoring databases. Homestead also supports multiple web servers and allows one to gracefully switch between them.

Instead of Vagrant’s traditional Vagrantfile, Homestead uses a `Homestead.yaml` file for configuration. This **file contains all of the configuration for our project** and can shared amongst a team to set up identical development environments.

Be aware that a Homestead instance **may results in a large virtual machine file**. It’s not unusual for this file to take up 5–15 GB of storage on the local disk. To achieve true dev site isolation, we might have to spin up multiple instances of Homestead. If our local machine only has a small SSD, this can present a serious disadvantage.

Website: [laravel.com/docs/7.x/homestead](https://laravel.com/docs/7.x/homestead)  
Supported operating systems: Linux, macOS, Windows


### <a class="anchored" id="valet">Laravel Valet</a>

![local-php-dev--valet](/dist/img/local-php-dev--valet.gif)

Valet is yet another technology by the Laravel project. However, it is not a Vagrant box and follows a radically different approach to local development: instead of setting up a development environment inside a virtual machine, Valet is **installed directly on top of the physical machine’s operating system**. This affords high performance, but also brings several serious downsides:

- Valet only works on specific machines and requires changes to the local system:

    > “Valet only supports Mac, and requires you to install PHP and a database server directly onto your local machine.”

- Valet relies on multiple services running on the local machine:

    > “Laravel Valet configures your Mac to always run Nginx in the background when your machine starts. Then, using DnsMasq, Valet proxies all requests on the *.test domain to point to sites installed on your local machine.”

It’s not hard to imagine that things can go seriously wrong with this kind of setup: any changes we make to our operating system or the Valet dependencies carries a **risk of breaking our development environment**. Since we’re not inside a virtual machine, we cannot just tear-down and re-provision. Good luck fixing Valet if it breaks.

That being said, when going with Valet one should make sure to **keep up-to-date full system backups**. Then just restore to a working version if the system breaks in any way. In conclusion, Valet may be a good choice for a developer working within a single, specific ecosystem. The makers of Valet advise that:

> “Valet isn’t a complete replacement for Vagrant or Homestead, but provides a great alternative if you want flexible basics, prefer extreme speed, or are working on a machine with a limited amount of RAM.”


Website: [laravel.com/docs/7.x/valet](https://laravel.com/docs/7.x/valet)  
Supported operating systems: macOS only

### <a class="anchored" id="docker">Docker</a>

![local-php-dev--docker](/dist/img/local-php-dev--docker.gif)

So far we’ve discussed virtual machine-oriented approaches. These provide great compartmentalization of our development environment, but can take up a lot of disk space and usually incur a noticeable performance hit. More modern solutions **ditch the virtual machine and employ sets of lightweight containers** instead. Containers provide an abstraction on top of the native operating system kernel, which yields a significant performance boost.

Each stack component is installed in its own container, which makes it easy to, for example, have multiple versions of a database running side-by-side. In theory, containers are the ideal solution, as they afford **perfect separation of development environments** while keeping performance high and disk usage low. However, in practice there are known Docker-specific issues:

- Docker Desktop on Mac and Windows uses a virtual machine, negating some of the performance benefits.
- Xdebug and symlinked repositories can be problematic with Docker.

Furthermore, setting up a development environment with Docker is technically challenging. Unless you’re super pro and know exactly what you’re doing, you most likely don’t want to go with pure Docker. It’s **probably a better idea to use an abstraction layer**, such as Lando or DDEV, to set up your container-based local PHP development environment.


Website: [docker.com](https://www.docker.com/)  
Supported operating systems: Linux, macOS, Windows

### <a class="anchored" id="lando">Lando</a>

![local-php-dev--lando](/dist/img/local-php-dev--lando.gif)

Lando is a powerful dev tool based on Docker. The basic idea is to allow us to **enjoy the benefits of Docker containers, without the headache** of having to configure them.

Development with Lando begins with a “recipe”. **A recipe is to Lando sort of what a box is to Vagrant**: a pre-defined set of technologies that are meant to be used together to run dev sites.

> “Recipes are Lando’s highest level abstraction and they contain common combinations of routing, services, and tooling”

The range of **Lando recipes encompasses different stacks**, such as LAMP, LEMP, and MEAN. One can also find specialized recipes for popular content management systems and web application frameworks. Whether looking to start a project using Drupal, WordPress, or Laravel, Lando has got you covered.

For general PHP development, we can start out with a LAMP recipe. Once we initialize our Lando project, a YAML config file is created for us. This so-called **“Landofile” contains all the configuration for our project**. Here, we can define our PHP version, ports and other network settings, environment variables, and the like. Generally, Lando strives to provide sane defaults via its recipes and offers mechanisms to allow us to override these defaults.

All in all, Lando appears to be a well-thought-out and mature solution. Besides easing the pains of local development, Lando strives to reduce the distance between the local dev environment and remote staging / production environments. Furthermore, Lando aims to allow an entire dev environment to be reproduced from configuration files alone. These properties make Lando an **attractive choice for team-driven, professional development**.

One word of caution: Lando for macOS and Windows ships with its own version of Docker Desktop, which **can cause problems if you already have Docker installed on your system**. Lando also has pretty [hefty hardware requirements](<https://docs.lando.dev/basics/installation.html#preferred>), which may present a serious barrier for some developers.

Website: [lando.dev](https://lando.dev/)  
Supported operating systems: Linux, macOS, Windows


### <a class="anchored" id="ddev">DDEV</a>

![local-php-dev--ddev](/dist/img/local-php-dev--ddev.gif)

DDEV is another dev tool based on Docker. The basic idea is the same as for Lando: provide a **comfortable configuration layer and sane defaults on top of Docker**. Instead of starting from scratch, we hit the ground running.

Unlike Lando, DDEV is **exclusively geared towards PHP development**. Although it lacks a concept of “recipes”, DDEV does provide specialized configurations for commonly-used PHP content management systems and frameworks. At the time of writing, DDEV comes with configuration support for the following systems:

- WordPress
- Drupal 6/7/8/9
- TYPO3
- Magento 1/2
- Laravel

The singular focus on PHP development simplifies things, as it allows the makers of DDEV to make more opinionated choices. Out of the box, DDEV includes useful tools, such as Xdebug, Ngrok, and MailHog. All in all, **DDEV feels more light-weight than Lando and may presently be the quickest solution** to getting a PHP dev site up and running.


Website: [ddev.com](https://www.ddev.com/)  
Supported operating systems: Linux, macOS, Windows

<mark>Please also see our [follow up post on how to set up DDEV for Craft CMS](/local-craft-dev-site-ddev-development-tool) in 15 minutes.</mark>


## In conclusion, what tool should we use to run our local dev sites?

The tools for setting up a local development environment all aim to solve a similar problem, but balance the tradeoffs differently. As such, there really is **no “one size fits all” perfect solution**. It is safe to say that each solution comes with its own advantages and disadvantages.

To get a better picture, we should expand our view beyond purely technical factors, and **include each solution’s ecosystem in our consideration**: can we rely on up-to-date documentation and ongoing development? Is it easy to find bug reports, answered StackOverflow questions, and blog posts on specific topics?

Furthermore, to find the right solution for our needs, **we need to ask ourself: what kind of development are we doing**? Are we exclusively building PHP sites, or using other languages as well? Within our language of choice, are we working mainly within a single, specific ecosystem, or are we developing using different frameworks and systems?

While it is difficult to give detailed recommendations, here’s a **condensed rundown of the technologies discussed, along with their strongest use case**:


### For most use cases go with…

- [**Homestead**](#homestead), if you're fine with using a virtual machine. Homestead offers a great ecosystem, so it's easy to find guides for setting up different PHP-based projects. Since Homestead runs on top of Vagrant, you can just add more boxes for development in other languages if needed. Keep in mind that each box eats up multiple gigabytes of disk space.

- [**DDEV**](#ddev), if you're only going to develop using PHP and want to get your site up and running as quickly as possible. This is an especially good choice if you're running Linux, as you'll get the full Docker performance benefit.


### If you have special requirements, consider…

- [**Vagrant**](#vagrant), if you need customizability above all else and are fine with using a virtual machine.

- [**Valet**](#valet), if you're looking to build a dedicated, single-purpose dev machine. This is the laptop you pick up every day for work. You don't use it to store personal documents, nor to manage a portfolio of diverse projects. Instead, you set this machine up for a single, long-running project, or to work on multiple projects within a single ecosystem.

- [**Docker**](#docker), if you need customizability above all else, or need to faithfully re-create a containerized production environment. For experienced users only.

- [**Lando**](#lando), for larger teams and professional deployments. Make sure your hardware is beefy enough for Lando to do its job. Unlike DDEV, Lando supports multiple languages via its recipes.

- **XAMPP** / **MAMP** / **WAMP**, for learning and experimentation. These are not a great choice for serious development, due to the lack of site isolation.


### Dev tool feature overview and comparison

Use this table to get a quick overview of the relative strengths and weaknesses of each tool.
Read the symbols as follows:

- `✓` Outstanding
- `⌀` Average
- `✗` Lacking

| Dev tool | Site isolation | Ease of use | Customization control | Low hardware requirements | High performance |
|:--              |:-:|:-:|:-:|:-:|:-:|
| **Vagrant**     | ⌀ | ✗ | ✓ | ⌀ | ✗ |
| **Homestead**   | ⌀ | ⌀ | ⌀ | ⌀ | ✗ |
| **Valet**       | ✗ | ⌀ | ⌀ | ✓ | ✓ |
| **Docker**      | ✓ | ✗ | ✓ | ⌀ | ⌀ |
| **Lando**       | ✓ | ⌀ | ⌀ | ✗ | ⌀ |
| **DDEV**        | ✓ | ⌀ | ⌀ | ⌀ | ⌀ |
| **XAMPP**       | ✗ | ✓ | ✗ | ⌀ | ✗ |