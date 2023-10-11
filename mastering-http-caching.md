---

author:     uk
created:    2017-02-24
title:      "Mastering HTTP Caching"
longtitle:  "Mastering HTTP Caching - from request to response and everything"
excerpt:    "Learn how to use CDNs as an easy-to-use edge cache."
lead:       "Using CDNs has long been something in the domain of the Alexa top 100; something a small(er) website does not need or cannot afford. This has changed over the last years, with a multitude of pay-per-use, non-enterprise vendors on the market CDNs became affordable for everybody. This article intends to show you how to get started with this easy to use caching variant."

keywords:   "cdn, caching, max-age, http, wordpress, cache-control, expires, pragma"
image:      "http-cache-poster.gif"

---


To use **C**ontent **D**elivery **N**etworks as HTTP caches you need to know about the proper HTTP response headers: Which are relevant? How do they work? How to you use them? All this I try to answer in this article.

The post does not claim to be exhaustive or even completely precise. In some instances, I will simplify and be opinionated for the sake of clarity, brevity and reduced complexity. This text handles the theory of caching - with a couple of practical examples, though. There will be follow up articles, building on this one, showing how to work with a CDN as caching layer with specific CMS or frameworks.


## Why use a CDN?

CDNs are intended as a globally distributed network to provide (not only) website contents faster to geographic locations, which are far from the actual infrastructure, which serves the actual content. For example: Your website is hosted in Ireland, your clients mostly sit in Australia. When a client visits your website the connection will suffer from latency leaving you with a sad client. Moving the (static) data to Australia with a CDN improves the client's experience.

However, CDNs are not limited to this use-case. As per their nature, CDNs are also a plain and simple cache; a **proxy cache** (or edge cache) to be precise. So, even if the geographic location part is non of your concern, you still should consider using the proxy cache aspect of CDNs to improve the experience of your users.


## Why use a Proxy Cache?

In short: Proxy caches take load of your web server and, since they are delivering only "static" content, are much faster. A simple example: Say you have a blog with a start page, listing all recent blog entries. To do that, a PHP script loads the latest blog entries from the database and renders them into an HTML result page. So for one request/visit: One PHP execution + a couple database queries. For a thousand requests/visits: a thousand PHP executions + a couple thousand database queries. Every PHP execution requires CPU, memory and I/O. Same goes for every database query.

The resource requirements scale linear with the amount of requests/visitors. Sounds good? It's not, because it will only scale linear up to a point: Any disk can only deliver so much I/O. Neither CPU nor memory are infinite. At some point, one of those bottlenecks will become critical and however much of the other resources you have won't matter: The website will become very slow, maybe even not responsive at all anymore. Sure, you can scale out horizontally, but that would make things a lot more complex, a lot more expensive and there is a much cheaper and far less complex solution:

A proxy cache in between allows you to mitigate resource limitations. Using the above example, with a proxy cache, only the first request would need to execute the PHP script, do the database queries and render the result HTML. All subsequent requests would be served from the cache. Cache access is basically direct memory access, which is about as fast as it gets. This means: the linear scaling problem is no more! A hundred visitors or a thousand visitors, it doesn't matter. Still only one PHP execution, one time database queries, one time rendering.


## CDN != CDN

There are various "kinds" of CDNs out there. Administrators would probably be most interested in where and how the data is stored and how the data is distributed within the CDN and differentiate by that. Since this is article is not addressed to administrators but developers let me just say that there are "classic CDNs" and "peer to peer CDNs", the latter being the modern approach.

From the developer perspective, it's more interesting how you get data into the CDN rather then how it then handles said data. In that sense, there are **push CDNs** and **pull CDNs** (also called "origin pull CDNs"). As their name implies, the push CDNs expect you to provide them the content while pull CDNs take care of fetching the content themselves.

This article will primarily address pull CDNs, because they are much simpler to implement and can, in many cases, be integrated transparently before an existing website without much effort.


## How pull CDNs work

Let's try an example and say you have a website, which is available under the URL `https://www.foobar.tld` to your visitors. In this scenario, the domain `www.foobar.tld` would be routed to the pull CDN server, not your web server. The CDN acts as **proxy** for the web server.

Another domain, which won't be publicly known, would route to the actual web server. Let's name it `direct.foobar.tld` for this example. The web server is called the **origin**.

The CDN now accepts any incoming request and either answers it directly from it's cache or delegates it to your web server, caches the response for future requests, and then delivers it to the client.

```
                 +-------+
                 |       |
                 | Cache |                                     [origin]
                 |       |                                direct.foobar.tld
                 +-^---+-+                                        |
                   |   |                                          v
+--------+       +-+---v-+                                  +------------+
|        +------->       +---------------------------------->            |
| Client |       |  CDN  |                                  | Web Server |
|        <-------+       <----------------------------------+            |
+--------+       +-------+                                  +------------+
                     ^
                     |
               www.foobar.tld
                  [proxy]
```

The most simplistic pull CDN would act as following:

* Get a request to `http://www.foobar.tld/some/page`
* Take `some/page` as cache key and check if it's already in the cache
* In cache: deliver result from cache
* Not in cache: request `http://direct.foobar.tld/some/page`, write response under `some/page` in cache and deliver


## Static vs dynamic content

The above setup works fine for completely static contents. Static contents means: Any data, which does not change for all visitors requesting the same URL. A good example would be assets, like CSS files. Say `http://www.foobar.tld/public/css/main.css`, where `main.css` is actually a plain file, which is the same for anybody visiting the site. Perfect for caching.

Opposed to static contents are, of course, dynamic contents. There are various reasons as to why content must be generated at runtime. Think, for example, about multi-language: Deliver contents based on the browser language. Also any kind of "user session" related content, such as switching the "Login" button with a "Logout" button when the user is logged in. You don't want that cached. Also don't forget about highly active contents as well: News pages, which change hourly or even more often, cannot be cached - or at least not for long.

Don't panic now. This is where it gets interesting, but still not hard to understand or implement:


## Cache headers

Most, if not all, pull CDNs allow you to address the issue of dynamic contents by allowing you to control the cache behavior "per page", or to even higher degrees (more on that later). To that effect, the simplest solution are good ol' HTTP response cache headers.

The first thing you should know about cache headers is that there are "old ones" and "new ones". Meaning: It was a process, not planed. New, in this case, means introduced with HTTP/1.1, while the old ones were specified with HTTP/1.0. Either way, the amount of available options lead to a lot of confusion about the whole topic and is in my opinion the single largest reason why people shy away from using cache headers.

To make it simple, let's concentrate on `Cache-Control` and `ETag`. Both are sufficient. Most CDNs still accept the "old ones" (`Expires`, `Pragma` and `Age`), but they are mostly used as a fallback, i.e. if you don't use the "new ones", then the "old ones" will be accepted.

### ETag header

Let's start with an easy one: `ETag`. It identifies the version of the document. Usually that means an MD5 hash over the content, but it could contain any value, representing the version/state of a document. Eg `1.0` or `2017-02-22`. One thing of note: The value must be double quoted, for example: `ETag: "d3b07384d113edec49eaa6238ad5ff00"`.

### Revalidation

Now to the practical application of `ETag`: revalidation. Let's forget the whole proxy + origin setup for a moment and just consider a simple client <-> server setup, to make this easy. Here is the setup:

```
+--------+       +------------+
|        +------->            |
| Client |       | Web Server |
|        <-------+            |
+--------+       +------------+
                       ^
                       |
                 www.foobar.tld
```

Now, let's further assume the client is making a request to `http://www.foobar.tld/hello.txt`. The server then serves the content with the following response:

```
# REQUEST
GET /hello.txt HTTP/1.1
Host: www.foobar.tld


# RESPONSE
HTTP/1.1 200 OK
Date: Sun, 05 Feb 2017 12:34:56 UTC
Server: Apache
Last-Modified: Sun, 05 Feb 2017 10:34:56 UTC
ETag: "8a75d48aaf3e72648a4e3747b713d730"
Content-Length: 8
Content-Type: text/plain; charset=UTF-8

the body
```

There are two interesting headers in response: Of course `ETag`, with the MD5 over the content and also `Last-Modified`, with a date of the last modification of `hello.txt`.

Now here is how revalidation works: When the client visits the URL again within a short time, the client's browser use one of those `If-*` request header, for example: `If-None-Match`, which checks against the content of `ETag`. This request header makes clear, that the client would accept either a full response or a response indicating that the content was not changed.

```
GET /hello.txt HTTP/1.1
If-None-Match: "8a75d48aaf3e72648a4e3747b713d730"
Host: www.foobar.tld
```

Now, if the `ETag` has _not_ changed, then the server could respond with:

```
HTTP/1.1 304 Not Modified
Date: Sun, 05 Feb 2017 12:34:57 UTC
Server: Apache
Last-Modified: Sun, 05 Feb 2017 10:34:56 UTC
ETag: "8a75d48aaf3e72648a4e3747b713d730"
Content-Length: 8
Content-Type: text/plain; charset=UTF-8
```

As you can see, this time the server response was not a _200 OK_, but a _304 Not Modified_, which omits the body and leads the client to use what was cached before. Sure, in case the body is only _the body_, as in this example, there is not much gained. But think of larger contents. Also think of expensive, dynamically generated contents.

As a developer, you might now think: _Not so great. Means that I have to handle those `If-` header in my application myself. More effort then before._ 

No worries. This is where the shared cache aka proxy aka CDN comes in. So going back to the original setup (client <-> proxy <-> origin). The proxy now is responsible for generating those _304 Not modified_ responses, based on it's cache. More on that in the following section. Before I get to it, a quick note on the `Last-Modified` header:

In this particular case, dealing with static content, which the `hello.txt` file is, the client could also have used `If-Not-Modified-Since: Sun, 05 Feb 2017 10:34:56 UTC` to achieve the same result (304 response). This works great with static contents, since the `Last-Modified` header in responses to static contents is automatically generated by the web server based on the modified timestamp of the file on the disk. However a modified date is often useless, because hard to determine, for dynamically generated contents. You know, the contents you want to have cached the most, because they are the most expensive to generate. So when developing, the `ETag` header is often a better choice.


### Cache-Control header

The `Cache-Control` header is a bit harder. It's harder for two reasons: first, `Cache-Control` can be used as request **or** response header. In this article, we only care about the response part, because this is what the developer has control of. Secondly, it controls potentially **two cache locations**: The "local cache" (aka "private cache") and the "shared cache".

The **local cache**, is a cache on the local disk of the machine running the browser. Your laptop, if you will. Be aware that you don't have "exact control" over that cache. Ultimately, the browser decides whether to follow your "suggestions" or not, which means: don't rely on it. The user might as well clear all caches whenever the browser is closed and you would not know about it, aside from increased traffic cause those caches invalidate faster then you anticipate.

The **shared cache**, is what this article is about: A cache in between the web server and the client. The CDN, in this case. You have full control over the shared cache and should leverage it to the fullest. Hence this article.

OK, let's dive in with some code examples. I'll explain in detail below:

1. `Cache-Control: public max-age=3600`
2. `Cache-Control: private immutable`
3. `Cache-Control: no-cache`
4. `Cache-Control: public max-age=3600 s-maxage=7200`
5. `Cache-Control: public max-age=3600 proxy-revalidate`

That might look a bit confusing, but don't worry, it's not that hard. First you should now that `Cache-Control` takes three "kinds" of directives: Cachability, expiration and revalidation.

First **cachability**, which takes care of the cache location, which in includes whether it should be cached at all. The most important directives are:

* `private`: Means it shall only be cached in the local (private) cache. On your laptop.
* `public`: Means it shall be cached in the shared cache. In the CDN. It can _also_ be cached on the local cache, though.
* `no-cache`: Interestingly this means caching is allowed - just everybody (local cache, shared cache) must revalidate before using the cached value
* `no-store`: Means it shall not be cached. Nowhere. Not ever.

Next up is **expiration**, which, obviously, takes care of how long things are cached. The most important directives are:

* `max-age=<seconds>`: Sets the cache validity time. How many seconds shall the cache location keep it? Goes for local _and_ shared cache.
* `s-maxage=<seconds>`: Overrides `max-age` just for the shared cache. No effect on local cache.

Lastly there is **revalidation**, which is, more or less, fine control. The most important directives are:

* `immutable`: Means that the document won't change. Ever. Can be cached until the heat death of the universe.
* `must-revalidate`: Means the client (browser) must still check with the proxy (CDN), even while it's cached!
* `proxy-revalidate`: Means that the shared cache (CDN) must check the origin, even while it's cached!

And to put it all together, here is how to read the above code examples in plain English:

1. Cache it both on CDN and laptop for an hour.
2. Don't store in CDN, only on laptop. Once cached (on laptop), no need to ever refresh it.
3. Don't cache it - or do. Just make sure to revalidate always!
4. Cache it for an hour on laptop, but for two hours on the CDN
5. Cache it both on CDN and laptop for an hour. BUT: if a request hits the CDN, although it's cached here for an hour, it still must check with the origin whether the document is still unchanged.


### Example

To break the monotony of theory, a short practical example on how to auto-inject `ETag` and `Cache-Control` headers. The example is meant for an Apache `.htaccess` file, but I hope you get the gist and are able to apply it to your web server of choice accordingly.

```
# Set ETag and cache for one day for all images:
<FilesMatch "\.(gif|flv|jpg|jpeg|png|gif|swf)$">
    FileETag -INode MTime Size
    Header set Cache-Control "max-age=86400 public"
</FilesMatch>

# Set ETag and cache for two hours, but assure revalidation, for all CSS, JS assets
<FilesMatch "\.(js|css)$">
    FileETag -INode MTime Size
    Header set Cache-Control "max-age=7200 public must-revalidate"
    Header unset Last-Modified
</FilesMatch>
```

Given the above, a response for the URL `http://www.foobar.tld/baz.jpg` would contain an `ETag` header, built from the modification time and size of the file, and a `Cache-Control` header with one day cache lifetime.

```
# REQUEST
GET /baz.jpg HTTP/1.1
Host: www.foobar.tld

# RESPONSE
HTTP/1.1 200 OK
Date: Tue, 07 Feb 2017 15:01:20 GMT
Last-Modified: Tue, 07 Feb 2017 15:01:15 GMT
ETag: "4-547f20501b9e9"
Content-Length: 123
Cache-Control: max-age=86400 public
Content-Type: image/jpeg
```

A response for the URL `http://www.foobar.tld/dist/css/styles.css` would also contain an `ETag`, based on modification time and size of the file, as well as a `Cache-Control` header with two hours cache time. Also the `Last-Modfied` header would be stripped, to assure that only `ETag` is used for revalidation.

```
# REQUEST
GET /styles.css HTTP/1.1
Host: www.foobar.tld

# RESPONSE
HTTP/1.1 200 OK
Date: Tue, 07 Feb 2017 15:00:00 GMT
Server: Apache
ETag: "20-547f1fbe02409"
Content-Length: 32
Cache-Control: max-age=7200 public must-revalidate
Content-Type: text/css
```


## Cookies

Now that you understand how caching headers work, let us consider how cookies play into caching. Firstly, Cookies are HTTP response headers. Namely the `Set-Cookie` header. The purpose of providing a cookie to a user is to identify the user, hence you _need_ a unique cookie per user.

When putting that in context of caching: Would you cache the response, including the `Set-Cookie` header, then every user (during cache time) would get the same cookie and thereby the same user session. [You don't want that](https://www.owasp.org/index.php/Session_hijacking_attack).

The other implication is that the user session state potentially changes the rendered content of the response. Simple scenario: Eshop basket. Based on the session cookie your application either renders no basket or renders a basket with the items this specific user has chosen. Again: You don't want that cached. Each customer should have their own basket, after all.

Having this said, don't confuse these session cookies with the more "benevolent" kind. A good example for the latter are Cookies set at runtime, via JavaScript. For example: Google Analytics integrated via JavaScript. GA sets a cookie (via JS), but this cookie does not impact rendering nor is there any `Set-Cookie` header involved. Even if GA would change the rendered site, eg by adding a small "you are tracked via Google Analytics"-icon, or something, it would not be a problem _as long as those changes are applied at runtime, in the browser and not by the (PHP) script in the background_.


### Dealing with cookies vs caching

First thing you should become aware of is how your web application (the underlying CMS/framework) works with cookies. Are cookies used sparsely, eg only during the login process? Are cookies injected into any response, on principle? Do you have control over when cookies are set?

To emphasize the previous section: Whenever you serve a response, which contains a `Set-Cookie` header, you want to make sure it is not cached. The same goes, when you render response, which contains "user specific" contents (eg the basket, from before). What this means depends on how CDN/proxy acts. For example:

* Does it support a default or fallback caching time, which is used to inject a `Cache-Control` header, if non is provided?
* Does it automatically strip any `Cache-Control` header, if `Set-Cookie` is present?

Once you know how your web application acts, regarding cookies, and what your CDN does, in terms of automagic, you can go about implementing your own defaults and preferences. Following an Apache `.htaccess` file example, which will help you getting started:

```
# 1) Enable caching, if COOKIE IS NOT used
Header set Cache-Control "public max-age=3600" "expr=-z resp('Set-Cookie')

# 2) Disable caching, if COOKIE IS used
Header always remove Cache-Control "expr=-n resp('Set-Cookie')

# 2a) Alternative to above: set caching to 0, if COOKIE IS used
Header set Cache-Control "no-cache max-age=0 must-revalidate" "expr=-n resp('Set-Cookie')
```

* Rule (1) sets the `Cache-Control` header with a default value, _if no Set-Cookie header exists_
* Rule (2) does the opposite: Strip `Cache-Control`, _if the Set-Cookie header does exist_
* Rule (2a) is a variant of the second, which sets an explicit 0-cache, instead of stripping the cache header.


#### Path based cookie suppression

Some CMS/frameworks seem to follow a brute-force'ish strategy, saturating generated responses automagically with an abundance of `Set-Cookie` headers. Whether setting those cookies with each and every response is necessary or redundant depends on various factors. For example session time: If you have a high security application with a very low session time of 5 minutes, then setting a new cookie with every response makes sense. If you not even have a "user space", i.e. everything is public and the same for every visitor, then setting any cookie (aside from tacking purposes) makes no sense.

So whether you can use the below example or not, depends strongly on your application. Either way, here we go. To give this example some context: Let's say you have a news website. All news posted news items are withunder `http://www.foobar.tld/news/item/<ID>`. Now you want to make sure that all responses to those `/news/item/<ID>` paths do not contain a `Set-Cookie` header, _because you made sure that those cookies are redundant_:

```
# the usual PHP redirect .. note the `?path=$1` in the rewrite rule
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ index.php?path=$1 [NC,L,QSA]
RewriteRule ^$ index.php [NC,L,QSA]

# using the previously set `path=` from the query
<If "%{QUERY_STRING} =~ m#path=news/item/[^&]+#">
    Header always unset Set-Cookie
</If>
```

For those who are interested: The redirect, using `path=$1` and the subsequent evaluation of `QUERY_STRING` are necessary in Apache, due to the execution order of the Apache directives. `If` is simply later evaluated then `RewriteRule`, so it cannot use the `REQUEST_URI` or anything of the original request, because that has already been changed due to the rewrite.


#### Cachability by design

There are design strategies to assure a web application is highly cachable. Since this is an article, and not a book, I cannot go into all, but let me highlight one commonly used for you:

Let's use the eshop example once more. Say there is a home page, which lists the top items for sale or something like that. Those top items are expensive to generate (lots of database queries), so you want them to be cached. The problem is the basket, from before, which should be rendered for logged-in users, but not for users which are not.

```
+----------------------------------+
| Welcome            +-----------+ |
|                    | 3 items   | |
| * Item 1 for $5    | in basket | |
| * Item 2 for $10   +-----------+ |
| * Item 3 for $7                  |
|                                  |
+----------------------------------+
```

The strategy would now be to first render the "generic" page, which every user, independent of the login state, sees. Then you load the unique basket via JavaScript and render it into the existing page. From the user's perspective, it looks the same eventually. Granted, instead of one request (render whole page, including basket) you now have two requests (render whole page + render basket). Still, you omit the "expensive" part, those top sales items, since that part is cached.

```
+----------------------------------+                   +----------------------------------+
| Welcome            +-----------+ |                   | Welcome            +-----------+ |
|                    | place     | |                   |                    | 3 items   | |
| * Item 1 for $5    | holder    | | ==[JavaScript]==> | * Item 1 for $5    | in basket | |
| * Item 2 for $10   +-----------+ |                   | * Item 2 for $10   +-----------+ |
| * Item 3 for $7                  |                   | * Item 3 for $7                  |
|                                  |                   |                                  |
+----------------------------------+                   +----------------------------------+
        [generic page]                                        [decorated with user]
```

This strategy, or variations thereof, is hard to apply to existing applications, cause it would change most of it's controller and probably most of the view layer (given a MVC layout). Best you make sure to do it from the start.


## Cache invalidation: Busting and purging

With the `max-age` and `s-maxage` directives, you already have detailed control on how long a specific response is to be cached. However, that's not sufficient in all cases. Those directives are set at rendering time. At this time, you simply might not know when the response should expire. Think for example about the home page a news website: Say, it contains the latest 10 entries. You set `max-age=900` for this home page, to make sure that is refreshed every 15 minutes. Now, one of the entries was published too early and shall go back to the drawing board again. You need a way to remove the cached response, so that it is refreshed now, not in 15 minutes.

 Don't worry, that's a common problem and there are tools to solve it. Let's first clarify the terminology:

* **Cache busting** means to circumvent the cache, by changing the cache key. Remember the (very) above example of `http://www.foobar.tld/some/page`, for which `some/page` would be used as the cache key? When changing the request to `http://www.foobar.tld/some/page?v2` the key changes to `some/page?v2`. Cache busted.
* **Cache purging** means to remove an item (aka a response) from the cache, so that it can/will/must be refreshed immediately.


### Cache busting with versioning

This strategy is very often used with assets (eg CSS, JS, ..). The idea is to include your assets using a version scheme. Those can be actual versions, a hash of the content, a timestamp and so on. To give you a few examples:

* Numeric versions: `style-v1.css`, `style.css?v=1`
* Hash as version: `style.css?d3b07384d113edec49eaa6238ad5ff00`
* Timestamp as version: `styles.css?t=1486398121`

What you need to consider is the context. In this case: the rendered HTML, which includes the CSS file via `<link rel="stylesheet" href="..">`, might be cached itself. So if your `style.css` is decorated with the latest version, it helps only if the CSS file is included using this latest version. If the HTML, which includes the CSS file, is served from the cache, it contains most likely the old version/file, so the old styles will still be served.


### Cache purging

How to purge one or multiple items from a CDN depends on the individual provider. Since many CDNs are built upon the open source software [Varnish](https://varnish-cache.org/), a common strategy is to use the `PURGE` verb in an HTTP request, for example:

```
PURGE /news/item/i-am-obsolete HTTP/1.1
Host: www.foobar.tld
```

Those purge requests usually require some kind of authentication or at least a source check (i.e. IP whitelist), but that depends on the provider.

While purging a single item, or a couple, is easy and fast there are scenarios in which that is not sufficient - or at least not elegant. For example, imagine a blog, which contains the author on most rendered pages. Now you change something in that "author block" and want to purge all "affected" pages. Sure, you can do that one-by-one, but if you have to purge a couple of thousand pages (ok, now leaving the blog example), then it can become harder.

The solution for that problem are:


#### Surrogate keys (aka Cache tags)

The name "surrogate keys" is used by the CDN provider [Fastly](https://www.fastly.com/) and I like it best, so I will go with that in this article. Other providers call them differently. For example "cache tags" is a popular choice. Varnish calls them [Hashtwo/Xkey](http://book.varnish-software.com/4.0/chapters/Cache_Invalidation.html#hashtwo-xkey-varnish-software-implementation-of-surrogate-keys), which is to cumbersome for me to use it here.

 However named, they serve the same purpose: Tagging responses with custom keys, so that you can purge them easily by those named tags, without even known what exactly has been cached.

To give you a quick example, using the client <-> proxy <-> origin layout, here is what your origin would respond with when using surrogate keys:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 123
Surrogate-Key: top-10 company-acme category-foodstuff
```

In this example, the response is "tagged" with three surrogate keys: `top-10`, `company-acme` and `category-foodstuff`. To give that some context, with the eshop example: This response contains the top 10 items of the shop, the product rendered in this response is from the company ACME and the category this product is in is foodstuff.

Having tagged the response, you can now easily purge all items in the cache which are tagged with `company-acme` or `top-10` or whichever custom context they are in. Easy, right?

How the actual purging is handled, again depends on the specific CDN vendor.


## Finish

That's about if for the theory. There will be follow up articles using specific CDN providers with specific CMS/frameworks. How many - we'll see. If you want to dig in now, here are some additional resources which you might want to read:


* [Google Developers: HTTP Caching](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=en#cache-control)
* [Push vs Pull CDN](http://www.whoishostingthis.com/blog/2010/06/30/cdns-push-vs-pull/)
* [CDN Types (admin perspective)](http://www.the-toffee-project.org/index.php?page=32-cdn-content-delivery-networks-types)
* [Cache headers overview (KeyCDN)](https://www.keycdn.com/support/http-caching-headers/)
* [Caching explained (Mozilla)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)
* [ETag header in detail (Mozilla)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag)
* [Cache-Control header in detail (Mozilla)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)
* [If-None-Match header in detail (Mozilla)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match)
* [Fastly: Surrogate keys](https://docs.fastly.com/guides/purging/getting-started-with-surrogate-keys)
* [KeyCDN: Cache tags](https://www.keycdn.com/support/purge-cdn-cache/)
* [KeyCDN: Cache headers](https://www.keycdn.com/blog/http-cache-headers/)

## Bonus

Learn how to [speed up APIs with HTTP Response Caching](https://blog.apisyouwonthate.com/speeding-up-apis-apps-smart-toasters-with-http-response-caching-a67becf829c6
) - the API client and your server will be grateful.
