---
author: os
created: 2018-03-28
title: "Your responsibility: App security"
intro: "Ultimately, you are responsible for your code and as well for the 3rd party code you rely on."
lead: "« Application security encompasses measures taken to improve the security of an application often by finding, fixing and preventing security vulnerabilities. » (Wikipedia)"
figure:
  src: security-advisories-header.jpg
tag:
  - webdev
head:
  meta:
    - name: 'keywords'
      content: 'php, composer, security'
---

A few days ago, late in the evening, we received a support ticket with the following message:

> My website nicesite.com and the <https://niceapp.frb.io> are being redirected to <https://some.paypal.fishing.site>. I haven't changed anything on the site in 2 months. It is not running a CMS and is a simple read-only php app. Have you been hacked?

The support team started the conversation with the client and checked the domain routing first. It quickly became clear that the redirects to the phishing domain happened on our platform, so they searched the access logs for suspicious requests. And they found this one:

```plain
[11/Mar/2018:00:42:20 +0000] 
POST "https://www.nicesite.com/root.php?edit=/srv/app/niceapp/htdocs/www/index.php" 
"Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.186 Safari/537.36"
```

After further communication with the client, the night shift decided to block HTTP requests to this App to prevent redirects to the phishing site. The state of the code base was archived for later.

I found the internal team notes and the related support case the next morning.

The `root.php?action=path/to/index.php` request smelled like a web shell, a little toolset to manipulate files on the server. **But how did it get there?** Unfortunately, we keep access logs not forever and the malicious code was created 4 weeks earlier. Therefore, the only source I had was the code.

Typical culprits for injections are outdated WordPress plugins, unguarded upload forms or
sloppy handling of [untrusted data](https://www.owasp.org/index.php/PHP_Security_Cheat_Sheet#Untrusted_data) in general. But I found a little neat application based on `twig`, `league/route`, `michelf/php-markdown`, a few controllers and some markdown files - very similar to our own [help.fortrabbit.com](https://help.fortrabbit.com) site. Everything felt very solid to me.

There is nothing wrong with the code, was my first impression. Then I discovered the public GitHub repo of nicesite.com, an exact copy of the hosted site, which included a little demo project in a sub-sub-folder. And this project included a `vendor` folder with a few dependencies, namely `symfony/http-foundation` and `phpunit/phpunit`.

**Long story short**, an unpatched phpunit (CVE-2017-9841), accessible via HTTP, as the vendor folder lived inside the document root, was most likely the entry point for the hacker.

I came back to the developer with my investigations. He patched his code immediately and replied as follows:  

> THANK YOU. I will definitely be recommending your service from now on. The other PaaS providers haven't been nearly as helpful.

## Takeaways

Ultimately, you are responsible for *your code* and as well as the 3rd party code you rely on.

There is a ton of information about Web Application Security on [owasp.org](https://www.owasp.org),
on [websec.io](https://websec.io/) Chris Cornutt covers the PHP world and here are the three takeaways I can provide from this particular case:

## Keep your dependencies up-to-date

Sensio Labs provides a [security checker](https://security.sensiolabs.org) that allows you check your dependencies for known security vulnerabilities,
via API, command line tool or web interface. The database does not include all composer packages, but the most common ones.

Download the .phar and make it globally executable to integrate this task in your workflow:

```shell
curl -O http://get.sensiolabs.org/security-checker.phar && \
chmod +x security-checker.phar && \
mv security-checker.phar /usr/local/bin/check
```

With this bash one-liner you can `check` all your projects at once from the parent directory:

```bash
for project in */; do check security:check "$project"composer.lock; done
```

## Prevent direct access to the /vendor folder

The following directory structure is very common when you use a framework like Symfony or Laravel:

```plain
.
└── htdocs
    ├── composer.json
    ├── composer.lock
    ├── vendor
    └── public << Your document root (www or web is common as well) 
```

As there is no need to access any PHP library directly, you should prevent it.
By following the structure above, a `index.php` is the only PHP file in the document root. The actual project code and the composer dependencies
are not accessible.
  
If your project dictates a different structure, with the `vendor` folder under the document root, prevent access - via .htaccess like so:

```xml
<Directory path/to/vendor/>
    Allow from None
    Order allow,deny
</Directory>
```

## Be aware that public repos are visible to everybody

Don't get me wrong, open source is great! But think twice before publishing something on github or other public repositories.
Crawlers, bots and even humans will find it. Not everybody has a white hat mentality and will let you know about possible issues.

Really important: Never store sensitive information like passwords or access tokens in git. Remember, git never forgets!
If you have committed sensitive information by accident, even if you revert the mistake, it will stay in the git history.
