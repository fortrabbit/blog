---
author: fl
created: 2016-06-15
title: TLS free launched
intro: Free SSL certificates for custom domains via Let's Encrypt are here now.
lead: SSL certificates for your custom domains by Let's Encrypt — <b>free and with zero config</b>.
figure:
  src: tls-free-poster.jpg
tag:
  - changelog
head:
  meta:
    - name: 'keywords'
      content: 'ssl, https, lets-encrypt, acme, CA, certificate authority, ACME, HTTP over TLS,HTTP over SSL, HTTP Secure'
---

**TL;DR** All custom domains with your fortrabbit (New) App can now also be served via `https://` with a valid certificate from Let's Encrypt unless a custom certificate is installed. Check out our [TLS help article](https://help.fortrabbit.com/tls) to learn more on implementation or continue here to read about what changes and a bit about the backgrounds.

![Browser Screenshot of TLS in action](/images/tls-free-screenshot.png)

## The changes

### TLS on fortrabbit so far

**Piggyback TLS for the App URL**: Free TLS for testing: Your fortrabbit App comes with an App URL (your-app.frb.io). This first address can already be accessed by HTTPS with a valid certificate provided by us, so you can develop your App to be HTTPS-ready.

**TLS custom**: Additionally you can book our TLS Component to bring your own custom certificate (from any CAs) and install it on the App for your custom domain.

### TLS on fortrabbit now

**Piggyback TLS for the App URL**: Stays as it is of course, as you might want to test HTTPS without routing a domain.

**TLS free**: Certificates from Let's Encrypt for every custom domain on your fortrabbit App are being issued, installed and renewed automatically. So you can use HTTPS on your own domains right away without configuration and for free.

**TLS custom**: Also stays as it is, as there are many use cases for this as well (see below).

### When to use TLS free

A quick and easy way to benefit from transport security for your App. Use it for small sites, hobby projects, during development for tinkering and for testing. No setup required, it's just there.

### When to use TLS custom

The more sophisticated, advanced way to achieve transport security. The setup is a bit more complicated and you need to purchase the certificate on your own as well as the TLS Component from fortrabbit. Your own commercial certificates can deliver a higher level of trust and they also offer some advanced configurations that are not possible with the free version (eg wildcard).

## Some backgrounds

### About TLS

TLS stands for Transport Layer Security and is the successor of SSL (Secure Sockets Layer). It's the cryptographic protocol that is used when you access a domain over a protected `https://` connection. HTTP happens on port 80, HTTPS on port 443.

Back in the days only business critical applications, like banking or e-commerce needed encryption. But nowadays Google and others are promoting to use "HTTPS everywhere" (for more online security).

### About Certificate Authorities

In order to communicate privately and encrypted, you need to know that your counterpart is who he claims to be. That's where certificate authorities (CAs) come into play: In essence, it's a chain of trust: they know somebody, who knows somebody, who knows somebody … who knows you. Pay a little money, send over a facsimile and they'll confirm that you are you. The more money you pay the more thoroughly they will check you out and the more your customers can trust that you are who you claim to be.

Classical CAs are: Comodo, Thawte, DigiCert, GeoTrust, Symantec, GlobalSign and StartSSL …

### About Let's Encrypt

[Let's Encrypt](https://letsencrypt.org/) is relatively new project aiming to bring certificates to everyone. It's a free, open and automated Certificate Authority. The service itself left beta in April this year. The Let's Encrypt setup is a bit different to classical CAs: the certificates only have a lifetime of ninety days. New certificates should be requested and installed automatically using a special client.

Developers really love Let's Encrypt and it already has a [market share of 0.1%](https://w3techs.com/technologies/details/sc-letsencrypt/all/all).

### Benefits of the fortrabbit implementation

You can install, configure and maintain such a client on your VPS yourself of course. But for fortrabbit clients it's part of the platform, just there for you to use. We take care of hosting and you of the coding.

---

Ok, this here is way below the fold. I am sure nobody is reading any more. So here is:

## My opinion (not fully aligned with my colleagues)

With this update we finally fulfill a frequent feature request. Traditional HTTPS is a hustle and means extra costs and DIY-lets-encrypt at least requires time, know how and responsibility. This update makes the fortrabbit even more attractive.

### Lowering entry barriers

**This is what I really like about it**: HTTPS is often a business requirement. But setting up TLS - by it's nature - was a complicated process so far: Creating keys and certs locally, purchasing certs from (shady-looking) external providers, Uploading keys … We tried to make the process as easy as possible, but it was still a hustle. So from a very complicated setup to no setup required at all is a major improvement. From costs on the fortrabbit side and on the external providers side to no costs at all is also a very good deal.

### Increasing general web security

**This is where I am bit sceptical**: There is [SNI](https://en.wikipedia.org/wiki/Server_Name_Indication), which enables multiple certs per IP making hosting HTTPS much more efficient and more affordable - we introduced that in December 2015. There is HTTP/2 which is only supported by browsers when running over HTTPS. Google, Apple and others pushing for a wider [HTTPS](http://techcrunch.com/2016/06/14/apple-will-require-https-connections-for-ios-apps-by-the-end-of-2016/) [adaption](https://www.youtube.com/watch?v=cBhZ6S0PFCY) — Chrome (Canary) and Firefox now even display a red icon when for HTTP-only-websites. And we have Let's Encrypt solving the big authentication obstacle.

On the other side, we have seen some serious security bugs in this space lately: [Heartbleed](https://en.wikipedia.org/wiki/Heartbleed), [Poodle](https://en.wikipedia.org/wiki/POODLE), [Drown](https://en.wikipedia.org/wiki/DROWN_attack) and now just recently the [Padding Oracle](https://en.wikipedia.org/wiki/Padding_oracle_attack).

So, we are in the middle of a security arms race. Now as HTTPS is becoming a commodity, what will that mean for security? Will HTTPS be as safe as CD copy protection or as secure WIFI protected by WPS?

### Further readings

Still don't have enough? Then you might also see my other rant article on the topic: [httpspeedy](/httpspeedy) with even more trade-offs.
