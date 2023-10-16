---

author:     fl
created:    2016-05-09
published: true
title:      "HTTP/2 reality check"
excerpt:    "How we tried to test the speed benefits of the new internet protocol."
lead:       'We have recently launched our <a href="/object-storage-launched">Object Storage</a> — an integrated S3-compatible asset storage. One of the features is HTTP/2 support. So we were curious to see the performance improvements: How much faster is it actually? TLDR: It depends. And it turned out that testing is never easy.'

keywords:   "S3, AWS, object storage, HTTP2, HTTP1.1, HTTP/2, TTFB, block storage"
image:      "http2-poster.gif"

---

## HTTP/2 expectations

HTTP/1.x — the rock on which the internet is build — is [really old](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#History). The [HTTP/2 standard](https://http2.github.io/) in comparison is a true youngster with it's [RFC](https://tools.ietf.org/html/rfc7540) being published in May of 2015. Nonetheless it is already supported by many [servers](https://github.com/http2/http2-spec/wiki/Implementations) and [browsers](http://caniuse.com/#feat=http2). A short recap on what HTTP/2 brings to the table:

* multiplexing: One TCP connection for multiple simultaneously requests
* header compression: reduced overhead
* binary: no text, just gibberish

We have all seen the impressive (and similar looking) demos from [CDN77](http://www.http2demo.io/) and [Akamai](https://http2.akamai.com/demo). So let's see what can we add to that.


## How we tested

The tests were developed around our internal discussions on the topic. They are just a quick sketch to investigate our assumptions. They were initially not meant for public - neither as a fancy demo, nor with a scientific approach. Still, we think they might be interesting so we decided to publish them anyway. All tests, unless specified otherwise, were run in various browsers: Chrome (50, 51, 52), Chromium (49), Safari (9.1.1) & Firefox (48).


## The Chuck Norris test

![Chuck Norris text](/dist/img/chuck-norris-test.gif)

Our first attempt was to rebuild the tests we have seen from others. Indeed, it worked well: You can obviously see how HTTP/2 delivers those 200+ images much faster - you don't even need a timer. That's sure looks like good marketing, but we're not if it answers any "real world questions".

* **[See the Slightly enhanced Chuck Norris test](http://http-test-2.frb.io/chuck-norris.html)**

## The extended test series

> Never trust a statistic you didn't forge yourself.

Ok, we admit, it was not only to test HTTP/2 - what we actually set out to do was testing our new Object Storage and compare it against our older implementation and other solutions. Here is what we asked:

* How does file size factor into the performance?
* How does TTL due to location factor in?
* How does delivery from local file system compares to Object Storage?
* How does our Object Storage compares to S3?
* How does our HTTP/2 implementation compares to other HTTP/2 services?

<figure style="margin: 3rem 0">
    <video autoplay="autoplay" controls="false" loop="true" style="border: 1px solid black; width: 100%">
      <source src="/dist/img/http2-tests-12-13-small.mp4" type="video/mp4">
      Sorry; your browser doesn't support HTML5 video in WebM with VP8 or MP4 with H.264.
    </video>
    <figcaption>
        Test 12 & 13 side by side with Chrome Developer Tools. <br>
        HTTP/2 (left) starts immediately but has a longer (green) Time-To-First-Byte.<br>
        HTTP1 (right) loads the images one by one, see the steps. <br>
        45 images load equally fast in both protocols in this test.
        </figcaption>
</figure>

* **[See all 20 extended tests](http://http-test-2.frb.io/)**

When running/looking at the tests yourself, mind:

### Caches

There are two caches involved here:

On the server side we have nginx, which stores frequent requests in memory and/or on local disk before handing the requests further down the rabbit hole. Cache busting, aka attaching a random query string, allows to circumvent that. There are tests with cache busting and without.

On the client side there is the web browser cache. In real-life scenarios this is a huge performance gain, but must be controlled in testing, of course. We used the Developer Tools to turn of local caching.

What was interesting for us, that circumventing the nginx cache did not reduce performance that much. Depending on the browser, the performance degraded between 0% and 30%. This merits further investigation - as does the gap in performance between browsers (later Chrome versions performed worse).


### TLS overhead

It would be interesting to see HTTP/2 over TLS and HTTP/2 over an unsecured connection. Unfortunately we cannot test that, as browsers only support HTTP/2 over TLS. So we tested: HTTP/2 (via TLS), HTTP/1.1 via TLS and HTTP/1.1 plain. Unsurprisingly HTTP/1.1 via TLS came out worst. Surprisingly HTTP/1.1 "felt" in many scenarios akin to HTTP/2. We assume this is because modern browsers already utilize multiple, concurrent connections to load page assets, which gives it a feel akin to TCP multiplexing.


### Location

Not a big surprise: The distance between the browser and the web server plays a major role. We have tested both of our data center locations US (Virginia) and EU (Ireland) from Berlin. We hoped that HTTP/2's TCP multiplexing would have a bigger impact, but — again — the concurrent requests browsers already make resulted in about the same experience.

<!-- Uli's theory  -->

In consequence: We already have ideas to extend our Object Storage by CDN functionality.


### Number of requests per page

How many assets will the average web application load? The fortrabbit marketing website currently loads about 55+ additional assets per page. That is actually quite slim, compared to other sites. Spiegel online, a major German news page, generates about 260 additional requests. So what is a realistic number here?

Today, we work around HTTP/1.1 limitations by: Inlining JS and CSS or even images; concating JS & CSS and even sharding assets across domains. Those techniques might become [anti-patterns](https://docs.google.com/presentation/d/1r7QXGYOLCh4fcUq0jDdDwKJWNqWK1o4xMtYpKZCJYjM/present?slide=id.p19) with HTTP/2, although they still would be more effective in some extreme edge case scenarios.

We think, that the trend will go towards more assets, leading to more parallel requests.

As expected, our tests revealed that HTTP/2's strength played out better with more concurrent requests: The earlier tests with 50 assets did not show much difference vs HTTP/1.1, but the tests with 200+ assets did. 

Again, we think that this might be because modern browsers already do concurrent requests with HTTP/1.1.

### Size and bandwidth

Size and bandwidth must, of course, be considered. The above tests contain some scenarios with large amounts of data, which should saturate most consumer uplinks easily. Once the bandwidth is saturated, there is not much HTTP/2 can to to improve the performance, of course. Unsurprisingly, this is what our tests showed as well.


### Type of elements

We — and most other HTTP/2 tests — have only covered to load a ton of images. A real life websites loads all kinds of stuff. Afaik, images are non-blocking: a web page will render without the images showing place holder icons and alt text. JS (unless loaded async) usually has to be downloaded in full. The same goes for CSS (can't even be asynced). How does it feel when those come over HTTP/2? We haven't tested that yet.


## Conclusions

I think we can safely say that HTTP/2 is not any slower than than HTTP1. And we also know by now that you should never ever trust any marketing buzz (including this one). 

Apart from that we conclude that our New Apps are much faster than our Old Apps and that New Apps combined with the Object Storage are even faster.

Never mind all this for your pet project. But maybe you are developing an image heavy eCommerce project? Then this might come in handy.

![Bush is doing it wrong](/dist/img/bush_doing_it_wrong.jpg)

Maybe we are just holding it wrong? You know better? Please call us, we are looking forward to hearing from you.


## WTF

Did you know that Google uses a `quic/1+spdy/3` protocol - based on UDP?


## Further readings

By the way, have you seen our [httpSpeedy](/httpspeedy) article from last year? Here we also reflect on "SSL everywhere" and "HTTP/2 trade-offs". In any case, check out [HTTP/2 Considerations](https://insouciant.org/tech/http-slash-2-considerations-and-tradeoffs/) by William Chan.
