---
author: js
created: 2020-09-10
title: Quickly set up a local Craft CMS dev site with the DDEV development tool
excerpt: Install the DDEV and power existing Craft CMS development sites.
lead: We will show you how to use the DDEV development tool to quickly set up a Craft CMS dev site for local development.
figure:
  src: ddev-poster.gif
tag:
  - webdev
---

## Introduction

### The DDEV development tool

A detailed introduction to DDEV was given in our previous [article on PHP development tools](https://blog.fortrabbit.com/tools-for-php-development-local-dev-site-setup#ddev). Maybe also check out the DDEV website at [ddev.com](https://www.ddev.com/).
To quickly sum up:

* DDEV is a Docker-based tool that **targets local PHP development**.

* DDEV supports a number of popular **content management systems and frameworks**.

* We can set up **DDEV with a standard LAMP stack for local Craft CMS** development.

### Installation requirements

DDEV sits on top of Docker and **works on macOS, Linux, and Windows**.
The installation will be shown for macOS.
To install on Linux you can also use Homebrew on Linux; the steps will be almost identical.
The same works for Windows, provided your system has the Windows Subsystem for Linux (WSL) installed.

For this installation procedure, you will need:

1. Basic knowledge of the **command line**.

2. PHP and Composer installed on the host machine.

3. The **Homebrew package manager** installed.

    * Install Homebrew on [macOS](https://brew.sh/)
    * Install Homebrew on [Linux or Linux Subsystem for Windows](https://docs.brew.sh/Homebrew-on-Linux)

## Install DDEV to power your local Craft CMS dev sites

First, we need to install DDEV on our machine.

The first step is to install Docker Desktop. If you already have Docker Desktop installed you can skip this bit.
One nice thing is that **DDEV tries to accommodate the Docker version** already installed on your system.
Other dev tools are less well-behaved in that regard.

```shell
# install Docker Desktop
brew cask install docker

# make sure to run the Docker App once before proceeding!
open /Applications/Docker.app/
# otherwise the ddev installation will not work
```

Once we have Docker installed we need to **launch the app at least once** to complete the configuration.
Next, we install DDEV using a custom homebrew “tap”:

```shell
# add custom ddev tap
brew tap drud/ddev

# install ddev
brew install ddev
```

If you're using a different operating system, or are uncomfortable using `brew`, check the official [DDEV installation](https://ddev.readthedocs.io/en/stable/#installation) instructions to find alternative means of installing DDEV.

## Set up a local Craft CMS dev site with DDEV

In this section we'll show how to **set up a brand new Craft CMS site with DDEV** for local development.
In case you want to use DDEV to power an existing local Craft dev site instead, please refer to our section [Using DDEV with an existing Craft CMS installation](#ddev-with-existing-site) below.

```shell
# create and enter project directory
mkdir craft-ddev && cd ./craft-ddev/

# use Composer to set up a Craft project
composer create-project craftcms/craft ./
# when asked if you are ready to set up craft, answer no, we will do it later

# create DDEV config
ddev config
# use the suggested defaults by hitting enter
# (<project-name>, 'web', 'php')

# spin up the machine the first time
ddev start
# this will take a while (once)

# once the machine is running we print out its settings
ddev describe
# note the network and database settings needed for the Craft setup
# this will also show how to connect to your site in the browser after setup

# log in to the running machine to set up Craft
# without this, the database connection will fail
ddev ssh

# set up Craft from inside the machine
# make sure to use the exact DB credentials as described from inside the container
./craft setup
# and leave the machine
exit
```

That's it. Now you should be able to **just access the URL shown via `ddev describe` in your browser** to visit your site.

## Using DDEV with an existing Craft CMS installation

We've shown how to use DDEV to set up a fresh dev site for local Craft CMS development.
Now you might be curious how to approach your existing local Craft dev sites.
Maybe you've been using Homestead or Valet so far, or another PHP development tool.
The good news is that it's really easy to **use DDEV to host your existing local Craft CMS dev sites** as well.
Here's how you run an existing Craft site via DDEV:

1. Use `cd` to enter your Craft project directory

2. Once there, run the following commands:

    `ddev config`

    `ddev start`

    `ddev describe`

3. Edit your `.env` file to reflect the values shown by `ddev describe`.

4. Access the URL shown by `ddev describe` in your browser.

You should be up and running with the Craft site showing in your browser.

## Deploy your local Craft CMS dev site

You've gotten your local Craft CMS dev site up and running — great!
But what's next?
Likely, you'll want to deploy your local site to your hosting provider.
So le'ts take a look at how to do that.
For this example, **we use our fortrabbit platform and the [Craft Copy tool](https://github.com/fortrabbit/craft-copy/)**.
With another tool and / or platform the exact specifics will differ.
But the general concepts should be similar.

### Requirement: have your SSH key set up

Here at fortrabbit, we care deeply about security.
Which is why we require our users to **connect to our infrastructure using an SSH key**.
This is contrast to logging in using a username-password combination.
To sync your local dev site to fortrabbit, you'll need to:

1. Have a public-private SSH key pair set up on your local machine.

2. Have the public key part connected with your fortrabbit Account.

If you're unsure about this, see our help pages for a [detailed instruction of how to set up the SSH key](https://help.fortrabbit.com/ssh-keys).

### Deploy a Craft CMS dev site to fortrabbit using Craft Copy

Once the SSH key is set up, we'll **configure DDEV to use the keys** from your local machine.
This will allow us to use Craft Copy from inside the container.
Just follow the steps outlined below:

```sh
# Make local SSH keys available inside the container
# ( Needs to be done each time you restart your machine )
$ ddev auth ssh

# Login to the DDEV container
$ ddev ssh

# Now, in the container, install and setup Craft Copy

# Required to get rid of PHP 7.0 for any Craft CMS lower than 3.6
$ composer config platform --unset

# Include Craft Copy via Composer
$ composer require fortrabbit/craft-copy -W

# Update dependencies first
$ composer update

# Install the plugin with Craft CMS
$ php craft plugin/install copy

# Initialize the setup
$ php craft copy/setup

# This will guide you through the steps and also run the initial installation

# Later on you can run the Craft Copy commands:
$ php craft copy/code/up
$ php craft copy/db/up
$ php craft copy/volumes/up
```

## Conclusion

In conclusion, **DDEV is a great choice for local Craft CMS development**.
DDEV can be used to quickly set up a new Craft CMS dev site and works just as well with your existing sites.
What's even better, DDEV plays nicely with Craft Copy.
In case you're already running Docker on your machine, having a local Craft CMS dev site powered by DDEV is just 15 minutes away.
We recommend you give DDEV a shot!
