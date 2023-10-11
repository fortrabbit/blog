---

title: "The perfect PHP platform manifest"
author: os
excerpt: "Looking for the perfect PHP hosting platform."
created: 2012/09/06 10:40:28

---


About 18 months ago the first players in the PHP Platform as a Service (PaaS) market got [some](http://clouduser.de/news/cloudcontrol-ist-live-5907) [media](http://techcrunch.com/2011/05/10/paas-php-fog-launches-to-the-public/) [attention](http://techcrunch.com/2011/08/23/engine-yard-acquires-orchestra-to-add-php-support-to-its-paas/), but they were far away from a perfect solution. At the same time our own hosting environment also wasn't satisfying in terms of deployment tools and scalability. So we started to collect ideas to improve our existing platform and ended up taking a big step forward a few months later:

  * Replacing our own hardware with AWS components
  * Completely rewriting 200K lines of codebase
  * New slim & extendable product structure
  * Strong focus on developer's needs

# Fortrabbit Manifesto

### for the perfect PHP Platform

#### Serve a fully managed & optimized stack

  * An extended maintenance-free LAMP stack
  * Bootable with a single click in seconds – a no-brainer
  * Stick to the latest stable versions (Apache 2.2 + PHP 5.4.6 at the moment)
  * A high level of security

#### Provide a functionally complete & flexible environment

  * Configurable settings (via GUI or ini_set())
  * Comprehensive set of PHP libraries
  * Scalable in any dimension (PHP/Database, Cache size, Multi-Level-Deployments)

#### Make the deployment process easy & fast

  * As quick as possible (push to deploy – done in seconds)
  * Stick to standards: GIT, SSH & (S)FTP
  * No proprietary tools/workflows

#### Provide tools for monitoring & analysis

  * Whats going on with my App? Is it healthy? Idle? Slow? And why?
  * And what can i do to make it perform better?

#### Give awesome support

  * Fast useful responses to support requests
  * Full documentation
  * Communication at eye-level

#### Offer it for a fair price

  * For the individual developer: with a small weekend-project
  * For the startup/company: with the need of scalibility & high availibility
  * For us: to pay the infrastructure and manpower to maintain & extend the service

This outlines our general philosophy for providing the service. Stay tuned for the second post where I go into more detail about how we're building a product following this manifesto, and why we're focusing on PHP rather than providing a platform that supports more programming languages - at least for the moment.
