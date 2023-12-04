---
author: js
created: 2021-05-27
title: "Craft Nitro 2 first look: How to quickly set up a local Craft CMS dev site"
intro: ""
figure:
  src: craft-nitro-poster.png
tag:
  - webdev
---

## Introduction

We previously tried out Craft Nitro when version 1.0 was released.
Due to the tool's reliance on the Multipass virtualization technology, we didn't get very far.
We ended up recommending [DDEV to run a local Craft site](https://blog.fortrabbit.com/tools-for-php-development-local-dev-site-setup#ddev) instead.
However, with the release of version 2.0, Craft Nitro has become an even more viable option.
Here we like to show you how to:

1. Get Craft Nitro 2 up and running on your machine.
2. Use Nitro to run existing or new Craft sites.

### Nitro 2 and Craft Copy: not ready to be best friends, at least not yet 😢

We had hoped to also be able to show you how to use fortrabbit's Craft Copy tool with Nitro to sync your Craft site to your fortrabbit Apps. Unfortunately, that's not currently possible due to some limitations in the environment Nitro provides. You can [read more about why at the end of this article](#craft-copy).

### The Craft Nitro 2 development tool

Made by Pixel & Tonic - the people behind Craft CMS - Craft Nitro 2 is:

* A Docker-based command-line tool for **local development**.

* Meant to be **easy to setup and use**.

* Unlike most other dev tools, Craft Nitro 2 is specifically geared towards **Craft CMS development**.

### Installation requirements

Craft Nitro 2 sits on top of Docker and **works on macOS, Linux, and Windows**.
The installation will be shown for macOS, using the Homebrew package manager.
To install on Linux you can also use Homebrew; the steps will be almost identical.
The same works for Windows, provided your system has the Windows Subsystem for Linux (WSL) installed.
For this installation procedure, you will need:

1. Basic knowledge of the **command line**.

2. The **Homebrew package manager** installed.

    ↳ Install Homebrew on [macOS](https://brew.sh/)

    ↳ Install Homebrew on [Linux or Windows Subsystem for Linux](https://docs.brew.sh/Homebrew-on-Linux)

We've **completed installation** using the following software / package versions:

| Software | Explanation | Version |
|:--|:--|--:|
| macOS Catalina | Operating system | `10.15.7` |
| zsh | Shell | `5.7.1` |
| Homebrew | Package manager | `3.1.4-22-gc11067c` |
| Docker Desktop | Container virtualization | `3.2.2` |
| Craft Nitro | Craft CMS dev tool | `2.0.7` |

## Install Craft Nitro 2 to power your local Craft CMS dev sites

The first step is to install Docker Desktop. If you already have Docker installed you can skip this bit.
At the time of writing, the **minimal supported Docker version is 3.0**.
Make sure to check the official [Craft Nitro 2 installation requirements][nitro-install] for up-to-date instructions.

1. Let's go ahead and **install Docker Desktop**:

    ```sh
    # install Docker Desktop
    brew cask install docker
    ```

2. Once we have Docker installed we need to **launch the app at least once** to complete the configuration.

    ```sh
    # make sure to run the Docker App once before proceeding!
    open /Applications/Docker.app/
    ```

3. Next, we **install Craft Nitro 2**:

    ```sh
    # install Craft Nitro 2
    brew install craftcms/nitro/nitro
    ```

If you're using a **different operating system**, or are uncomfortable using `brew`, check the official [Craft Nitro 2 installation instructions][nitro-install] to find alternative means of installing Craft Nitro 2.

### Things to consider before setting up Craft Nitro 2

Having installed Docker and Craft Nitro 2, we continue by initializing Nitro.
The initialization procedure is interactive;
we'll be asked to make a few **basic choices, such as which database(s) to use**.
The choices made during initialization are saved in the `'.nitro/nitro.yaml'` file inside the user's home directory.
As such, Craft Nitro 2 settings are user account-specific.

Before we can get started, we need to answer a couple of questions:

1. Do you have **another dev tool installed** on your machine?

    Nitro's default settings require ports `80` and `443` to be available.
        If another dev tool, such as DDEV or Lando, is already installed these ports will likely be taken.
    In this case, we'll have to use custom ports for Nitro.

2. Are you **working under an account with admin privileges**?

    Nitro wants to edit the hosts file when initializing.
    This requires `sudo` privileges, so initialization needs to be run as an admin user.

    A standard macOS user account has admin privileges enabled. However, [recommended best practice](https://www.bsi.bund.de/DE/Themen/Verbraucherinnen-und-Verbraucher/Informationen-und-Empfehlungen/Cyber-Sicherheitsempfehlungen/Basisschutz-fuer-Computer-Mobilgeraete/Basisschutz-fuer-Computer/Benutzerkonten/benutzerkonten_node.html) is to work under a non-admin account.
    If you're not working as an admin user, you'll need to turn off host file editing and add the hosts file entries yourself.

### Initializing Craft Nitro 2

For this installation procedure, we'll assume that we're on a machine:

* with other **dev tool(s) installed**,
* working as a **user with admin privileges**.

Before starting the initialization, **we'll set custom ports for Craft Nitro 2**.
We'll also explicitly tell Nitro to use the `'.nitro'` top-level-domain (TLD) for its local host names.
We apply these customizations by setting a few [Craft Nitro 2 environment variables](https://craftcms.com/docs/nitro/2.x/customizing.html#nitro-environment-variables) to appropriate values.
To do so, we copy the following commands into a terminal and run them:

```sh
# set environment variables
export NITRO_HTTP_PORT='8080'
export NITRO_HTTPS_PORT='8443'
export NITRO_DEFAULT_TLD='nitro'
# uncomment next line to turn off hosts file editing
# export NITRO_EDIT_HOSTS='false'

# initialize Craft Nitro 2
nitro init
```

Once the environment variables have been set, **we continue to initialize Craft Nitro 2**.
Again we're asked to make a number of choices.
These will depend on your specific setup;
we've documented ours here:

| Craft Nitro 2 `init` step | Value |
|:--|:--|
| Would you like to use MySQL [Y/n]? | `y` |
| Select the version of MySQL | `1` (MySQL 8.0) |
| Would you like to use PostgreSQL [Y/n]? [Y/n] | `n` |
| Would you like to use Redis [Y/n]? | `n` |

## Set up a local Craft CMS dev site with Craft Nitro 2

In this section we'll show how to **set up a fresh Craft CMS site with Craft Nitro 2** for local development.
In case you want to use Nitro to power an existing Craft CMS dev site, please refer to the section [using Craft Nitro 2 with an existing Craft CMS installation](#existing-craft-site-with-nitro2) below.

We'll use the `'nitro create'` command to set up a local Craft CMS dev site.
This command uses Composer inside the container, so there's **no need to have Composer installed locally** — nice!
Please refer to the [official Craft CMS installation guide][craft-install] for other means of installing.
We'll kick of creation of our new Craft CMS site via the following command:

```sh
# create a new Craft CMS dev site on the Desktop
cd ~/Desktop && nitro create fortrabbit
```

The `'nitro create'` command runs interactively, presenting us with a set of choices.
We've documented ours here:

| Craft Nitro 2 `create` step | Value |
|:--|:--|
| Enter the hostname [fortrabbit.nitro] | `<Enter>` |
| Enter the webroot for the site [web] | `<Enter>` |
| Choose a PHP version | `1` (PHP 8.0) |
| Add a database for the site [Y/n] | `y` |
| Enter the new database name | `fortrabbit` |
| Should we update the env file? [Y/n] | `y` |

After creation, a new container for our site should be up and running.
We can test this by issuing the `'nitro ls'` command.
This command **lists all running Nitro containers** along with their status.

Let's continue by setting up Craft CMS.
To do so, we'll **log into the site's container and run the Craft CMS setup** from there.
Since we asked Craft Nitro 2 to update the site's `.env` file, we want to use those settings.
Use the following set of commands to get your site set up.

Make sure to **adapt the settings** underneath ">>> provide your site settings here <<<" to suit your needs.
We recommend you copy-paste each commented block of code into your terminal and run them there.

```sh
# log into the container
nitro ssh fortrabbit

# make sure we're in the correct directory
cd /app/

# load existing settings from .env file
source .env

# run Craft CMS database setup in non-interactive mode
# using settings loaded from .env
./craft setup/db --interactive=0 --driver='mysql' --server="$DB_SERVER" --port="$DB_PORT" --database="$DB_DATABASE" --user="$DB_USER" --password="$DB_PASSWORD"

# >>> provide your site settings here <<<
adminEmail='craftadmin@fortrabbit.nitro'
adminUser='craftadmin'
adminPassword=$(openssl rand -base64 32)
siteName='fortrabbit Craft Nitro'
siteUrl="http://fortrabbit.nitro:8080"

# install Craft CMS in non-interactive mode
./craft install --interactive=0 --email="$adminEmail" --username="$adminUser" --password="$adminPassword" --siteName="$siteName" --siteUrl="$siteUrl" && printf "\n- Your password for user '${adminUser}' is:\n\n${adminPassword}\n\n-Your site should be live at:\n\n${siteUrl}\n\n" && exit
```

A couple **things to note**:

* We've **initialized Craft Nitro 2 using custom ports**.

    We need to append the port number to the site URL: `http://fortrabbit.nitro:8080/`. Otherwise, our site won't load.

* We've used the **settings stored in the `.env` file**.

    For debugging, we can print out those settings while inside the container by issuing a `'cat /app/.env'` command.

Our site should now load in the browser — **make sure to test it works**!

## Use Craft Nitro 2 to power an existing Craft CMS dev site

Maybe you'd like to **run an existing Craft CMS project via Craft Nitro 2**.
In this case, we'll use the `'nitro add'` command instead of `'nitro create'`:

1. Go to your local Craft CMS project directory:

    ```sh
    cd <craft-project-dir>
    ```

2. Add the site to Craft Nitro 2:

    ```sh
    nitro add .
    ```

    Here, we're given a similar set of choices as for the `'nitro create'` command.
    You may find our choices in the section on [setting up a new Craft CMS site](#new-craft-site-with-nitro2).

3. Import your local database backup:

    ```sh
    nitro db import <path-to-your-SQL-backup>
    ```

<!--

## Sync your local Craft CMS dev site with your fortrabbit app

* employing fortrabbit's own [Craft Copy tool](https://github.com/fortrabbit/craft-copy/)

* <https://blog.fortrabbit.com/craft-copy-1-released>

* we previously showed how to do this using DDEV

* Nitro brings a couple useful commands to the table
* using the `'nitro composer'` and `'nitro craft'` commands
* allows us to run `composer` and `craft` inside the container

* here we ran into an issue
* Craft Copy syncs all components of a Craft site, up and down
* uses Git and Rsync with SSH keys under the hood
* need to associate local SSH keys with the container
* currently, Nitro lacks this capability
* although Nitro 1.0 had a `'nitro keys'` command
* presumably similar to DDEV's `'ddev auth ssh'` command

* how to get SSH keys into the container <https://github.com/craftcms/nitro/issues/297>

* at time of writing, the only way to use Craft Copy with Nitro 2.0
* is to run Craft Copy from outside the container
* not preferred:
* forces us to have all of Craft Copy's dependencies installed on our local machine
* opens the door for version conflicts, etc.
* detracts from the advantage of using Nitro:
* container encapsulation, dedicated commands like `'nitro composer'`

* prepare our system for running Craft Copy

```sh
# install Craft Copy dependencies locally
brew install git rsync php composer mysql-client
```

```sh
# Required to get rid of PHP 7.0 for any Craft CMS lower than 3.6
nitro composer config platform --unset

# Include Craft Copy via Composer
nitro composer require fortrabbit/craft-copy

# Update dependencies first
nitro composer update

# Install the plugin with Craft CMS
nitro craft plugin/install copy

# ---- check requirements before proceeding ---

# prepare our system for running Craft Copy locally
brew install git rsync php composer mysql-client

# Initialize the plugin
./craft copy/setup

# Once installed, run the Craft Copy commands:
./craft copy/code/up
./craft copy/db/up
./craft copy/volumes/up
```

-->

### Craft Nitro 2 and Craft Copy

Over the years, fortrabbit has contributed to the Craft CMS ecosystem.
We've published plugins, guides and blog posts.
The latest exciting development is fortrabbit's own [Craft Copy tool](https://blog.fortrabbit.com/craft-copy-1-released).
Craft Copy **syncs all components of a Craft site, up and down**.
This includes your custom code, as well as assets, database contents and the Craft CMS code.
As an added bonus, Craft Copy supports advanced use cases, such as [multiple staging environments](https://github.com/fortrabbit/craft-copy/#multi-staging-config).

We previously showed how to [integrate Craft Copy with DDEV](https://blog.fortrabbit.com/local-craft-dev-site-ddev-development-tool#deploy-to-hosting-platform).
Naturally, we attempted to do the same with Craft Nitro 2.
Unfortunately, here we ran into an issue.
Craft Copy uses Git and Rsync with SSH keys under the hood.
To use the tool, one **needs to install the SSH keys associated with your fortrabbit account within the container**.
To our surprise, Craft Nitro 2 lacks the capability to import SSH keys from the host machine — [see this GitHub issue](https://github.com/craftcms/nitro/issues/297). It also does not have the other dependencies (`ssh`, `rsync`, `zcat`) available inside its container that Craft Copy needs in order to work.

At time of writing, the only way to use Craft Copy with Craft Nitro 2 is to run Craft Copy from outside the container.
But this is not preferred:
using the tool outside the container **requires its dependencies to be installed on the user's local machine**.
Such an approach opens the door for version conflicts and similar headaches.
Certainly not something we want to recommend.

That said, Pixel & Tonic have a great track record of responding to demand from the Craft CMS community, so it's possible they will update Nitro in future to allow better integration with other tools. If this is something you'd like to see, consider [letting them know](https://github.com/craftcms/nitro/issues/).

## Conclusion

A fair share of fortrabbit's client base use our infrastructure to host their Craft CMS sites.
This includes less technically-minded folks, for whom setting up a local dev sites is a real challenge.
So we'd love to have a **single, integrated solution to recommend**.
Initially, Craft Nitro 2 looks really promising in this regard.

Craft Nitro 2 ships with a handful of useful commands, including
`'nitro composer'`, `'nitro php'`, `'nitro craft'`, and `'nitro npm'`.
These allow us to issue `composer`, `php`, `craft`, and `npm` commands inside the container.
This absolves the user of the responsibility of installing and maintaining these tools on their own machine.
Instead, the **dependencies live inside the container**.
We love it, as that reduces the surface area for version conflicts and related confusion.

While **Craft Nitro 2 does a good job** at quickly getting a local Craft CMS dev site up and running, when it comes to the more sophisticated aspects of Craft CMS development, DDEV still pulls ahead.

We really hope to see Host SSH key support added to Craft Nitro 2 soon.
When that happens we'll be happy to give it another shot.
For now, we'll **continue to recommend DDEV to our clients** as the go-to solution for local Craft CMS development.

Summing up, here are some of the **strong points of Craft Nitro 2 and DDEV** compared:

| Feature | Nitro | DDEV |
|:--|:--|:--|
| Supports Craft CMS | Explicitly | Implicitly via PHP recipe |
| Set up as non-admin user | Doesn't seem to be supported | Straightforward via admin account |
| Use local host names | Requires editing hosts file | Implemented via `*.ddev.site` lookup |
| Dedicated commands for dependencies inside container | Craft, Composer, PHP, NPM | Composer, PHP |
| Use SSH keys inside container | Currently unsupported | Supported via `ddev auth ssh` |

<!--

* nice: `'nitro create'` command sets up Craft site

* not so great: custom ports need to be set via environment
* when initializing Nitro
* instead of config file
* where we could look up / adjust those values
* hosts file editing requires admin privileges
* (DDEV uses clever trick via `*.ddev.site`)

* turning off hosts file editing is unreliable
* even when the environment variable is set, some commands still attempt to edit the hosts file
* requires Ctrl-C to abort, can lead to inconsistent project state

* `'nitro remove'` supposed to remove a site
* but seems to be broken in current version
* subsequent `'nitro ls'` shows container still running
* need to manually delete container via Docker dashboard

* `'nitro destroy'` failed to export database backup
* should abort in this case, but continued
* could be disastrous in some cases

* installing and using Nitro without `sudo` privileges not great
* goes against recommended best practice

* <https://www.bsi.bund.de/DE/Themen/Verbraucherinnen-und-Verbraucher/Informationen-und-Empfehlungen/Cyber-Sicherheitsempfehlungen/Basisschutz-fuer-Computer-Mobilgeraete/Basisschutz-fuer-Computer/Benutzerkonten/benutzerkonten_node.html>

----

```sh
# create and enter project directory
mkdir ~/Desktop/craft-dev/ && cd ~/Desktop/craft-dev/

# use Composer to set up a Craft project
composer create-project craftcms/craft ./
# when asked of you're ready to set up Craft, choose 'no'
```

* ran into known Composer / PHP issue on macOS Catalina:

> - craftcms/cms[3.6.4, ..., 3.6.12] require ext-zip * -> it is missing from your system. Install or enable PHP's zip extension.

* trying to resolve issue
* using <https://stackoverflow.com/a/58300437>

1. Re-install PHP

    ```sh
    # from admin user account
    brew update
    brew install php@7.3
    brew link php@7.3
    ```

2. Set up paths

    ```sh
    # from your own (!) user account
    echo 'export PATH="/usr/local/opt/php@7.3/bin:$PATH"' >> ~/.zshrc
    echo 'export PATH="/usr/local/opt/php@7.3/sbin:$PATH"' >> ~/.zshrc
    ```

3. Open a new terminal window and check your PHP installation

    ```sh
    # should report '/usr/local/opt/php@7.3/bin/php'
    which php
    # should report '7.3.xx'
    php -v
    # should return 'zip'
    php -m | grep zip
    ```
----

1. Retrieve information about Nitro containers:

   ```sh
   nitro ls
   ```

2. Copy the hostname of container with type 'Database'.

   In our case this was `mysql-8.0-3306.database.nitro`

3. Add entry to hosts file:

   ```txt
   127.0.0.1 mysql-8.0-3306.database.nitro
   ```

----

* we turned off hosts file editing via environment variable
* add hostfile entry for the `.nitro` domain:

```txt
127.0.0.1 fortrabbit.nitro
```

* to edit the hosts file you'll need `sudo` access
* if  VS Code is installed
* there should be a `code` command on the command line
* otherwise, we'll use `nano`
* then we can edit the hosts file with the following commands

```sh
# open terminal session as admin user
su <your-admin-account-name>
# load the hosts file into editor via `sudo`
sudo code /etc/hosts
# sudo nano /etc/hosts
# make your changes and save the file normally
```

* (personally, I prefer using Sublime Text for hosts file editing)
* attempting to save a sudo-access file in Sublime opens a convenient prompt
* supply admin name and password
* file gets saved

----

```sh
# Login to the container
nitro ssh

# Now, in the container, install and setup Craft Copy

# Required to get rid of PHP 7.0 for any Craft CMS lower than 3.6
composer config platform --unset

# Include Craft Copy via Composer
composer require fortrabbit/craft-copy

# Update dependencies
composer update

# Install the plugin with Craft CMS
php craft install/plugin copy

# Initialize the setup
php craft copy/setup
# This will guide you through the steps and also run the initial installation

# Once installed, run the Craft Copy commands:
php craft copy/code/up
php craft copy/db/up
php craft copy/volumes/up
```

BONUS: Now, you might want to deploy your local Craft CMS installation to some hosting provider. For this example, we use our fortrabbit platform and the  but some concepts might be of general interest:

### Requirements

*  Use SSH key auth - not username/password
*  Have some SSH keys installed on your host machine 
*  Have your pub key part is connected with your fortrabbit Account

More details on SSH key setup with fortrabbit here: [help.fortrabbit.com/ssh-keys](https://help.fortrabbit.com/ssh-keys)

## References

* <https://jamesmacwhite.medium.com/nitro-2-the-docker-powered-development-environment-for-craft-cms-2bb59728844e>

* [Official Craft Nitro 2 Installation Guide][nitro-install]
* [Official Craft CMS Installation Guide][craft-install]

-->

[nitro-install]: https://craftcms.com/docs/nitro/2.x/installation.html "Installation | Craft Nitro Documentation"

[craft-install]: https://craftcms.com/docs/3.x/installation.html "Installation | Craft CMS Documentation | 3.x"
