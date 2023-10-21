---
author: js
created: 2020-10-14
published: true
title: A first look at the new Craft Nitro development tool
excerpt: The new tool by Pixel & Tonic, can we recommend it yet?
lead: 
image: craft-nitro-poster.png
imagecredit: ""
tag:
  - webdev
---

Previously, we explored a variety of dev tools in our [article on local PHP development](https://blog.fortrabbit.com/tools-for-php-development-local-dev-site-setup).
We narrowed our focus to [setting up a Craft CMS site with the DDEV development tool](https://blog.fortrabbit.com/local-craft-dev-site-ddev-development-tool).
Here, we examine if the new Craft Nitro local dev tool will also fit our purpose.

DISCLAIMER: this article reflects the author's opinions and is based on their experience testing Craft Nitro on macOS while adhering to common best practices.

## An overview of the Craft Nitro development tool

Nitro caught our attention during a recent [devMode.fm Podcast](https://devmode.fm/episodes/boost-your-local-development-with-nitro) dedicated to this new development tool.
The [introductory blog post](https://craftcms.com/blog/craft-nitro) on the Craft CMS homepage states that:

> “Nitro is a speedy new local development environment that’s tuned for Craft CMS, powered by Multipass.”

So, what does this mean?
First of all, **Nitro is a command line tool.**
**It consist of a single executable** installed to `/usr/local/bin/`.
To achieve this level of simplicity, Nitro uses a local virtual machine (VM) based on Canonical's “Multipass” Ubuntu virtualization technology.

Nitro strives to make local development easy and deliver high performance for local Craft dev sites.
Additionally, Nitro tries to **balance ease of use with the ability to customize it**.
In the words of one of the Nitro developers comparing Nitro to other dev tools:

> “Every solution sucks in its own unique way — Nitro tries to be the one that sucks the least”

From the devMode.fm Podcast episode we learned that Pixel & Tonic, the company behind Craft CMS, are pushing towards a Laravel-like ecosystem, with best practices in place for common use cases.
From the perspective of the Pixel & Tonic team, a **large percentage of Craft support requests are related to both local development** and production config.
For less technically-inclined users, getting something like [Homestead](https://blog.fortrabbit.com/tools-for-php-development-local-dev-site-setup#homestead) up and running can be a challenging process.
With Craft Nitro, Pixel & Tonic hope to level the playing field for new Craft developers.

### Craft Nitro Features

We previously discussed [best practices for setting up a local dev site](https://blog.fortrabbit.com/tools-for-php-development-local-dev-site-setup#local-dev-site-setup).
Most solutions offer a way to script and automate the setup process of a local development environment.
With VM-based tools, this process is known as “provisioning” and consists of two components:
the provisioning software, and a user-editable configuration file.
For Craft Nitro, the environment **configuration is held in a YAML file that adheres to the “Cloud Init”** industry standard.

Broadly speaking, most local dev tools fall into one of two categories: those based on a virtual machine, and those based on Docker containers.
Craft Nitro employs a hybrid approach:
it uses a **virtualized Ubuntu instance, but additionally runs Docker inside the VM**.
This allows Nitro to work with and seamlessly switch between different database versions, as each version runs in its own Docker container.

Like other popular dev tools, Craft Nitro is controlled via the command line.
It offers a [host of useful commands](https://craftcms.com/docs/nitro/commands.html), such as `db backup` and `db import`, to backup and restore a database snapshot, respectively.
A single instance of Craft Nitro **can be used to power multiple Craft sites**, and there's also a convenient option to host an entire folder of existing Craft CMS projects.
In the future, Craft Nitro might get a graphical user interface (GUI), making it even more accessible for developers and designers looking to quickly set up a local Craft site.

As previously mentioned, Craft Nitro runs on top of the Multipass virtualization technology.
This innovative piece of software is made by Canonical, the company behind the popular “Ubuntu” Linux distribution.
**Multipass uses the operating system's native hypervisor**, which promises a significant performance boost when compared with non-optimized virtualization tools.

### Installing the Multipass virtualization technology on our local machine

On a Mac, **Multipass can be installed with a single [Homebrew](https://brew.sh/) command**:

```bash
brew cask install multipass
```

The same should work on a Linux system, for which [Homebrew is also available](https://docs.brew.sh/Homebrew-on-Linux).
For other operating systems, or if Homebrew is not available, the **installation may be carried out using one of the installers provided** on the Multipass homepepage:

* [multipass.run](https://multipass.run)

We first **attempted to install Multipass on a Mac using Homebrew**, but quickly ran into a Multipass permissions error:

```
multipass socket access denied
Please check that you have read/write permissions to '/var/run/multipass_socket'
```

For context, we adhere to the **best practice of operating a main user account without admin privileges**, with a separate privileged user account set aside for administrative tasks.
With this setup, software can normally be installed via the Homebrew package manager when logged in as the admin user.
Once installed, the software can be used by a non-admin user as well.
Unfortunately, this does not appear to be the case with Multipass.

Since our Homebrew installation attempt was unsuccessful, we tried the installation again, this time using the package installer from the Multipass homepage.
Unfortunately, **we got the same permissions error when starting Multipass**.
To work around the "multipass socket access denied" permissions error thrown by Multipass, we used the following code:

```
# For this to work on macOS there must be two user accounts:
#
# non-admin user:   <your user name>
#     admin user:   <your admin user name>
#

# start session as non-admin user
# and save user name for later
user=$(whoami); export user

# edit your admin user name below
admin="<your admin user name here>"

# log in as admin user — will ask for your admin password
su "$admin"

# add non-admin user to group `wheel`
# sudo commands may ask for your admin password
sudo dseditgroup -o edit -a "$user" -t user wheel

# change group ownership of multipass socket to `wheel`
sudo chown :wheel /var/run/multipass_socket

# give read-write permissions to `wheel` group members
sudo chmod 775 /var/run/multipass_socket
```

Please note that we're changing permissions and group membership, so there may be security implications.
**This code is included here for educational purposes only**;
use at your own risk.

### Installing and initializing Craft Nitro on our local machine

Once Multipass has been installed, **installing Craft Nitro should be a breeze**.
All we need to do is open up a terminal, log in as an admin user and run the following commands:

```
# edit your admin user name below
admin="<your admin user name here>"

# log in as admin user — will ask for your admin password
su "$admin"

# under admin account
bash <(curl -sLS http://installer.getnitro.sh)
```

This will **download and execute the Craft Nitro installer script**, which will place the `nitro` binary on our system.
Then, under a normal user account, we initialize the Craft Nitro machine using the following command:

```
# initialize Craft Nitro machine
nitro init
```

Running the command spawns an interactive prompt, which lets us choose the following:

* How many  **processor cores** to use for the VM.
* How many **Gigabytes of RAM** to use for the VM.
* The amount of **disk space** allocated to use for the VM. You will need a minimum of 4 GB for the installation.
* Which **database engine** to use for the VM.
* Finally, which **database version** to use for the VM.

Once we've chosen the desired values, Craft Nitro will proceed to download multiple large files.
On our first try the **installation failed due to missing packages**.
Upon further inspection, we found a bug report stating [“make sure you are not on a VPN”](https://github.com/craftcms/nitro/issues/127#issuecomment-634347495).
We switched off the VPN and ran the initialization again.
This time it worked and took about ten minutes to complete.

### Adding a local Craft CMS project to Craft Nitro

Once the Craft Nitro machine has been set up, we **proceed to adding an existing Craft CMS project**.
For this purpose, Craft Nitro provides the convenient `nitro add` command.
Running this command inside a Craft CMS project directory will again spawn an interactive prompt:

```
# navigate to Craft CMS project directory
cd <path-to-craft-project>

# add the Craft CMS project to the Nitro machine
nitro add
```

During this part of the process we were asked to provide additional details, such as the desired **host name for the site and the webroot directory**.
Craft Nitro tries to make this as easy as possible by providing sensible defaults.

### Multipass issues preventing us from using Craft Nitro on macOS

Unfortunately, when attempting to add a site to Craft Nitro we again ran into a Multipass permissions issue.
At this moment, we felt it was prudent to look a bit deeper into Multipass, as it is the critical software component that Craft Nitro depends on.
We discovered that **Multipass has a few serious issues under macOS at the moment**:

* On macOS, the [Multipass VM file is stored outside of the normal macOS folder structure](https://github.com/canonical/multipass/issues/566). This is a serious problem, as VM files should normally be stored in a directory that is excluded from Time Machine backups.

* The official Craft Nitro documentation states, [“Multipass requires Full Disk Access on macOS”](https://craftcms.com/docs/nitro/usage.html#adding-sites). Again, this seems problematic and is unusual when compared with most other dev tools.

* For people running the popular “DNSMasq” tool on their machine, [Multipass can run into DNS issues](https://github.com/craftcms/nitro/issues/127#issuecomment-626239432). DNSMasq is a crucial component of the widely-used dev tool “Laravel Valet” and needs to be stopped in order to run Multipass.

Considered together with the aforementioned permissions errors, we concluded that **Multipass is not a viable choice for most use cases on macOS at the moment**.
Since Craft Nitro requires Multipass to run, we were unable to complete the setup and failed to use Nitro to power our local Craft CMS dev sites.

## Conclusion

Nitro looks really promising, but is hamstrung by the underlying Multipass issues.
Maybe on Linux or Windows this works out differently. However, **on macOS the problems seem too much of a hassle to work around** for us.
After all, one of the main requirements we have for any dev tool is to [“Isolate the development environment from our physical machine’s operating system.”](https://blog.fortrabbit.com/tools-for-php-development-local-dev-site-setup#local-dev-site-setup)
Having to set up special permissions, or run the software as an administrative user clearly goes against this basic rule.

That being said, do keep an eye out!
**If Multipass matures Craft Nitro might still be a great choice** for local Craft CMS development.
For the time being, [we recommend to use DDEV instead](https://blog.fortrabbit.com/local-craft-dev-site-ddev-development-tool).
It's a great tool that runs on top of Docker and doesn't suffer from any of the problems we encountered with Multipass.
As usual, there's an exception to this general recommendation:
if you're a Craft developer who uses a Mac and who has never heard of `sudo` and doesn't use separate admin and user accounts, you might want to give Craft Nitro a shot. If you do so, we'd love to hear about your experience!
