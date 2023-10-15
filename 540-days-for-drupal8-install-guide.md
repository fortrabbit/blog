---

author:     fl
created:    2016-08-25
published: true
title:      "Our Drupal 8 install guide took 540 days"
longtitle:  "Our Drupal 8 install guide took 540 days"
excerpt:    "What took us so long to come up with a Drupal 8 install guide."
lead:       "Why it took us such a crazy long time to write an <a href='https://help.fortrabbit.com/install-drupal-8'>install guide for Drupal 8</a>."

keywords:   "CMS, install-guide, Drupal8"
image:      "drupal8-poster.gif"

---

We maintain a couple of [install guides](https://help.fortrabbit.com/#install-guides) to help our clients to get started with their CMS or framework on our hosting service quickly. So we have some superficial knowledge about modern and popular PHP CMS/frameworks. 

**Drupal 8 is a huge step forward.** It features modern, object-oriented code (classes, inheritance, interfaces), requires a least PHP 5.5.9, makes use of PHP standards  (PSR-4, namespaces, traits), Symfony components, PHPunit integration, Twig, HTML5, Guzzle, Assetic, file system abstraction and more. We were quite exited about Drupal 8, from the first Beta on — as we saw it to be a good fit for our platform.



### Timeline

* 2014-10-01 - [Drupal 8 Beta 1 released](https://www.drupal.org/blog/drupal-800-beta-1-released) — yeah!
* **2015-02-18** - first draft of our Drupal 8 install guide
* 2015-02-15 - [Our first Drupal 8 landing page](https://web.archive.org/web/20150228101028/http://www.fortrabbit.com/drupal-hosting) — in good hope
* 2015-08-01 - [Discussion on how to use Composer with Drupal 8](https://www.drupal.org/node/2551607) — hhhm
* 2015-10-04 - Clients frequently request Drupal 8 infos — sorry not yet
* 2016-03-14 - [Composer issues with Drupal 8 fixed](https://www.drupal.org/node/2648064) - new hope
* 2016-04-12 - Problems getting Flysystem to work with [Object Storage](https://help.fortrabbit.com/object-storage)
* 2016-05-27 - We submit [a feature request](https://www.drupal.org/node/2735253) to support 3rd party S3 providers
* 2016-06-24 - We [ask to help](https://twitter.com/fortrabbit/status/746305157076553728) with the feature request
* 2016-07-21 - Our feature requests goes upstream > [drupal 8.1.x-dev](https://www.drupal.org/project/drupal/releases/8.1.x-dev) — Thank you!
* **2016-08-03** - We finally release our [Drupal 8 install guide](https://help.fortrabbit.com/install-drupal-8)


### Conclusions

There are some differences between CMS and framework install guides. Frameworks are mostly easily to install and configure, CMS are more complex and need more steps to install and tune. Drupal 8 is a huge ecosystem. We have much respect for the community efforts to move it forward to a modern PHP while still taking care about the legacy.

Our current version of our Drupal 8 install guide is far from perfect. It's missing tuning tips and a way on how to integrate Memcache. We are thankful for bug reports and contributions (source is on [GitHub](https://github.com/fortrabbit/help/blob/master/docs/install-drupal-8.md)).

Thanks again to the Drupalists who helped us come so far.
