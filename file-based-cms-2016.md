---
author: fl
created: 2016-06-07
published: true
title: File-based CMS overview
excerpt: Thoughts on flat file CMS and static site generators, mostly PHP-related.
lead: Let's have a look at different types of database-less CMS — the candidates, the pros, the cons and what you need to consider when it comes to deployment & hosting.
keywords: headless, lambda, flat-file, database-less, file-based, blog aware, weblog, textile, non-DB, no-db, twig, prototyping, service manuals, decoupled CMS
image: flat-file-cms-poster.gif
tag:
  - opinion
---

### Manifesto

* Skip the database
* Dump the rich-text WYSIWYG editor
* Write text files in Markdown
* Store meta data in the text file as a front matter YML block
* Use Git (and Composer) to manage and deploy


### Scope

A **developer-friendly** Content Management Systems for: blogs, simple websites, themes, components, docs, gh-pages, prototypes, click-throughs … you name it. I'd like to split those systems in two different flavors:

## Static site generators

A static site generator will parse all your contents to build plain HTML pages out of it. For a blog it will turn the Markdown source files to HTML using templates and also generate archive lists. 

**It's a radical concept after more then 20 years of server-side scripting.** The HTML files can be generated on your local machine and then deployed to any web server that can render HTML, no PHP, Ruby or Node required. Let's fight [website obesity](http://idlewords.com/talks/website_obesity.htm): Simple HTML pages can of course be rendered faster using less computing resources.

As a static site generator is actually a task runner, it can be build with anything — Gulp for example. And it can also compile to anything — the output format can also be an e-book.

### Example candidates

[Jekyll](https://jekyllrb.com/) is the most known candidate - it's integrated in GitHub (GitHub pages). But there are many more: [StaticGen.com](https://www.staticgen.com/) lists 143 different systems. [Sculpin](https://sculpin.io/), [Couscous](http://couscous.io/), [Spress](http://spress.yosymfony.com/) are in PHP.
### My experience

We have used [Metalsmith here for a while](https://blog.fortrabbit.com/new-blog-layout) but eventually ditched it. Each build process generated 100 of HTML pages. It was fast, but still an extra step.
### Deployment & hosting

At minimum you want the exported folder uploaded and served somewhere. 

#### Static site hosting

* use GitHub pages for this and route your domain there (free)
* setup a task that deploys all files to an AWS S3 bucket and route your domain there (cheap)
* store those files in Dropbox folder and route the domain (free i think)

Please consider that you want to have the source code that creates the files as well as the original markdown files backed up. With the GitHub pages way this is solved (master branch contains source, gh-pages the generated stuff), Dropbox has it's own backup-magic, for the AWS way you might find something else. 

#### With fortrabbit

1. pragmatic: put everything in Git and deploy it all together, route your domain to the output folder
2. clean: define the built process to run as a post-deploy script, after each deploy (of course only when using a PHP generator)


----


## Flat file CMS

**Flat file CMS are static site generators without the static part.** Rendering is done dynamically — using server-side scripts. Each time a user requests a certain resource, a HTML page will be built: combing templates and the actual contents from the Markdown files. Still no database: all reads are done from the local file system. Of course this requires some more computing power from the web server and thus can not be as fast as delivering raw HTML pages as with the pre-generated sites. But clever caching can help to deliver even complicated queries fast — humans will not spot the difference. 

So: still the same look and feel, but without that tedious built process.


### Candidates

| Name                                   | Established | License | GitHub Stars | Twitter | 
|----------------------------------------|-------------|---------|--------------|---------| 
| [Baun](http://bauncms.com/)            | 2015        | 0       | 200          |         | 
| [Bludit](https://www.bludit.com/)      | 2015        | 0       | 120          |         | 
| [Grav](https://getgrav.org/)           | 2014        | 0       | 4300         | 2900    | 
| [Herbie](https://www.getherbie.org/)   | 2014        | 0       | 30           |         | 
| [HTMLy](https://www.htmly.com/)        | 2014        | 0       | 430          | 6       | 
| [Kirby](https://getkirby.com/)         | 2009        | $15     |              | 4000    | 
| [Monstra](http://monstra.org/)         | 2012        | 0       |              | 400     | 
| [Phile CMS](http://philecms.com/)      | 2013        | 0       | 200          |         | 
| [Pico CMS](http://picocms.org/)        | 2013        | 0       | 2000         | 20      | 
| [Pulse](https://www.pulsecms.com/)     | 2015        | $39     |              | 500     | 
| [Sphido](https://www.sphido.org/)      | 2014        | 0       | 160          |         | 
| [Stacey](http://staceyapp.com/)        | 2009        | 0       | 1000         |         | 
| [Statamic](https://statamic.com/)      | 2012        | $200    |              | 2600    | 
| [Yellow](http://datenstrom.se/yellow/) | 2013        | 0       | 200          |         | 


There are many more, but these well known (in PHP) and actively maintained. 

### My experience

I did a small project in Grav and liked it. Grav is still a bit rough around the edges and feels like an Open Source project here an there — but that's exactly what it is. The good documentation, the demo templates, plugins and the community helped me getting up fast.

We also use custom flat file generation for this blog and our [help pages](https://help.fortrabbit.com) using some custom micro scripts based on [Slim](http://www.slimframework.com/). So I probably would prefer a flat file CMS over a static site generator for these kind of tasks and when being with other developers.

We work with Git subtrees to separate code from content. The content of our documentation is a [public repo hosted on GitHub](https://github.com/fortrabbit/help). We pull this into an App to generate the layouts. But that doesn't help with the admin-dashboard case.
### Deployment & hosting

Some **flat file CMS** are providing browser-based wordpress-like admin panels. And I totally get why: The "client" should be able to use it as well. That changes deployment & hosting a lot:
#### With fortrabbit

Files created on the server are breaking compatibility with our hosting service and most other PaaS. Our New Apps have [ephemeral storage](https://help.fortrabbit.com/quirks#toc-ephemeral-storage). Any file manipulation on a remote server will be lost on each new deploy or change of settings and is only done on one Node, where the App can run on multiple Nodes (horizontally scaled).

The immediate reflex is to think: Hey, let's store those Markdown texts in a database! Isn't it better to separate the code from the contents anyways? Well, maybe. But then it's not file-based anymore, that's just a regular CMS. 

**Other possible hacks**

* save `*.md` files to a remote file system (S3 or [Object Storage](https://help.fortrabbit.com/object-storage) in our case); 
* commit changes from the admin panel to Git again so that new contents can be pulled.

**Bottom line**: You can't really host a flat file CMS in a 12-factor environment: when new contents get generated on the server (client mode). But you can perfectly host it here: when you skip the admin-dashboard and content & code live together in a repo and you deploy it all together (dev style).


#### With classical hosting

> Code moves up. Content moves down.

In a classical hosting scenario you might have the following setup: The newest source code comes from your local machine, to update the server you upload the changed files manually, or use Git and then ignore the folders containing the actual contents. Then you possibly need to find a way to move the latest content down to your local development environment (as a backup and to have the local dev close to production) — or you just rely on the backups your hosting partner provides.

Bottom line: A flat file CMS can be hosted in a classical hosting environment, but you need a good strategy to merge content and code together.


## Wrapping up

**Separation of presentation and content** is something file-based CMS are not about in the first case. The beauty of those systems is the pragmatic **get-the-job-done-quickly**-without-too-much extras-and-tech-evolved approach. Old-school CMS like WordPress are doing a better job in separation, as the content is (mostly expect for uploads which hasn't been covered here at all and is a topic of it's own) in the database. 

Markdown text files on disk — on the other hand — are very accessible, they make sense even alone without the presentation layer. 


## Headless CMS to the rescue?

![Headless animated GIF](/dist/img/headless.gif)

Let's see what an upcoming wave of decoupled, api-based CMS will bring us. I want these three layers: 

* **Engine**: back-end makes an API available
* **Content**: Data in a portable format
* **Presentation**: Front-end templates and styles


