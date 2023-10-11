---

author:     fl
created:    2015-11-05
title:      "httpSpeedy?"
excerpt:    "HTTP/2 expectations and pitfalls"

---


> The future is here, it's just not evenly distributed yet.

William Gibson


TLDR: This article is about the acronyms TLS/SNI, HTTP/2 & CAs and why not to make hasty changes.

We are running and building our PHP hosting platform here. The fun part for my job is to evaluate new technologies. So I recently did some research into the next version of the Hyper Text Transfer Protocol. Here are my learnings.

Disclaimer: I am not a hardcore techie.


## 1. Hello TLS & SNI

To establish a HTTPS connection (on a custom domain) we currently offer SSL termination, which is implemented as a dedicated load balancer. The product is a bit pricey, since we buy it pricey. It is also all too complicated for my personal flavor. But soon, we are going to release a SNI based TLS variant. It basically does same, but we can install multiple certs on a single load balancer which enables us to offer the service for a more affordable price. So far so good, now how can we improve further?


## 2. Hello HTTPS/2

The Apache web server project recently announced support for HTTP/2. So I needed to have another look. Without wanting to go into all the techie details: overall HTTP/2 sounds promising. Faster page delivery (just think of multiplexing) without any code changes — as it is fully backwards compatible. And it already has a huge browser support. So what is holding us back?


## 3. Hello "Let's Encrypt"

One thing that bothers me is the shady [Certificate Authority](HTTPS://en.wikipedia.org/wiki/Certificate_authority) business. You know these 90ies-style websites were you pay to get a double-opt-in email and some text-blob-strings (the actual certs). 

The [Let's Encrypt](HTTPS://letsencrypt.org/) initiative may soon make this obsolete and may bring mass adaption of secure website connections — HTTPS; a commodity.


## My obvious conclusion

All browsers are supporting HTTP/2 only over a secured connection. Now the idea simply was to combine those three technologies above to a seamless experience on our platform:

HTTP/2 everywhere, custom domains must be routed over HTTPS which is fairly simple to set up and doesn't even cost extra. Everything is more snappy, more secure. We have something to play for the early adapters and even better Google rankings for our clients (as rumored).


## Hello tech trade-offs

I learned that HAproxy (our load balancer of choice) is expected to support HTTP/2 fully with the next release version 1.7 which is expected not sooner than September 2016. We shortly discussed switching to NGINX for that reason.

While continuing my research I stumbled over the excellent article by Will Chan: **[HTTP/2 considerations and tradeoffs](HTTPS://insouciant.org/tech/http-slash-2-considerations-and-tradeoffs/)**, which marked a turning point in my thinking. Read it, if you have couple of hours.

I learned about the major technical considerations when implementing HTTP/2: [Network performance](HTTPS://insouciant.org/tech/http-slash-2-considerations-and-tradeoffs/#NetworkPerformance), [Scalability & DoS](HTTPS://insouciant.org/tech/http-slash-2-considerations-and-tradeoffs/#ScalabilityDoS), [Complexity](HTTPS://insouciant.org/tech/http-slash-2-considerations-and-tradeoffs/#ImplementationComplexity), [Binary protocol](HTTPS://insouciant.org/tech/http-slash-2-considerations-and-tradeoffs/#TextBinary), [Deployability](HTTPS://insouciant.org/tech/http-slash-2-considerations-and-tradeoffs/#Deployability).

These reasons alone scared me enough not to start a field test with this new technology in production. But the most interesting part — for me at least — was the non-techie part:

## Hello political considerations

The article also gave me insights into the process of agreeing on specifications. I learned how much such a technical topic is driven by the "special" interests and opinions of the involved parties.

I used to think that HTTPS — end-to-end encryption — everywhere is a good idea, as it is a general privacy improvement. I am not so sure about this any more:

> "SSL everywhere" is security snakeoil: The CA system is broken, trojaned, corrupt and unsalvageable. 

[Poul-Henning Kamp](HTTPS://twitter.com/bsdphk/status/659485236473044992) - FreeBSD, Varnish …

I don't believe in conspiracy theories all that much. But in post-Snowden times (and today on Guy Fawkes night), we probably should think twice when it comes to security and privacy. Many [comments](HTTPS://www.schneier.com/blog/archives/2014/11/a_new_free_ca.html#comments) on the article by Bruce Schneier about Let's Encrypt suggest not to trust this free service, just because of the involved companies. Alternative free CA solutions might be:

* [CAcert](http://www.cacert.org/): community certificates (not trusted by browsers by default?)
* [StartSSL](https://www.startssl.com/): commercial CA provider with a free version (looks oldschool)

## My learnings

On a personal level I was reminded to question the things around us. I personally would prefer anonymity not only privacy when surfing most of the web. 

On a professional level the same applies. We need to make careful decisions in the interest of our clients. Just the same with PHP7: we will wait until it is ready for production.

## Furher readings

* [Is TLS fast yet?](https://istlsfastyet.com/)
* [The US government https only standard](https://https.cio.gov/)
* [HTTPS everywhere](https://www.eff.org/HTTPS-EVERYWHERE): browser extension to brut-force https connections
* [HTTP/2.0 — The IETF is Phoning It In](https://queue.acm.org/detail.cfm?id=2716278): ACMqueue article (2015)
* [Security Collapse in the HTTPS Market](https://queue.acm.org/detail.cfm?id=2673311): ACMqueue article (2014)
* [Making the Web Faster with HTTP 2.0](http://queue.acm.org/detail.cfm?id=2555617): ACMqueue article (2013)
* [HTTP Performance Is a Solved Problem](http://www.infoq.com/presentations/HTTP-Performance): Talk by Poul-Henning Kamp