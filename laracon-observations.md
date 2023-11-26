---
title: Laracon observations
excerpt: What we have learned on the Laracon conference 2013 in Amsterdam.
author: fl
figure:
  src: laracon.jpg
created: 2013-09-02
published: true
tag:
  - opinion
---

# We've been to Laracon

What happens when you gather together some of the most influential PHP framework developers? The Laracon conference in Amsterdam was the answer to this question.

### Symfony Laravel relationship

It surprised me a bit, when I saw Symfony creator [Fabien Potencier](https://twitter.com/fabpot) even before the Laravel author [Taylor Otwell](https://twitter.com/taylorotwell) on the speakers list. I never really thought about the relation between Symfony and Laravel. Laravel uses Symfony components, sure, but where is the connection? Isn't there some kind of competition going on? On the first day there was a spontaneous Q&A session with Taylor, and he was asked just that: _How are you connected to Symfony, is there an official partnership agreement?_ His answer was along the lines of: _Well, actually we just use their components, but we don't really contribute back._ I was wondering how Fabien felt about this? Later on I was surprised to learn from Fabien that this is actually part of his plan. He has decoupled his framework into single, stand-alone components, so that other projects can easily leverage them as their building blocks. Drupal8 is another good [example](http://symfony.com/blog/symfony2-meets-drupal-8) for this. The idea is simple: Why should each framework reinvent the wheel for certain problems that are already solved in a great way elsewhere? This way the Laravel core team can focus on what they are really good at. The other big benefit is of course compatibility: With many frameworks using, say, the [HttpKernel](https://github.com/symfony/HttpKernel) component, you already know how it works. So if you start a Drupal (8) project tomorrow, you already understand the core, if you've worked with Laravel or Symfony before. Of course, without [Jordi Boggianos](https://twitter.com/seldaek) work resulting in Composer - the middleware, if you will - all of this would not have been possible. We are really excited about all this and curious where this all will lead to in the future. Maybe we'll see more specialized "meta" frameworks, solving edge cases, 'cause they become even more easy to build? Maybe even real standard components, outside the PHP core, which everybody uses so that you can rely upon them? 

### On event organisation

Thanks again to [Shawn](https://twitter.com/ShawnMcCool), [Jereon](https://twitter.com/JeroenGerits) and the whole Laracon team: You really did a great job! We have had a blast! I really liked the format of the conference. The location was great and everything worked just smooth and flawless. Even the WiFi didn't broke (very much). The ticket price was not too high and not too low. Cheaper tickets would have allowed more people to attend, which would have been maybe very nice, but on the other hand maybe more noisy and stressy for everyone. This way it was a very intimate atmosphere under high professionals. 

### More impressions

[Ben Rey](http://twitter.com/bjmrey) did a very nice summary of [day 1](http://storify.com/bjmrey/laracon-europe-amsterdam-30-31-august-2013) and [day 2](http://storify.com/bjmrey/day-2-laracon-europe-amsterdam-30-31-august-2013) with many tweets, quotes and slides. See [photos from Jordi](http://www.flickr.com/photos/seldaek/sets/72157635332125877/) and [photos from Stefan Neubig](http://www.flickr.com/photos/emotional-stuntman/9642114207/) on flickr. 

Go Laravel!