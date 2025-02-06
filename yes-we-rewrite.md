---
title: Yes, we rewrite
author: fl
created: 2025-02-06 20:25:35
intro: Reflecting on our decision to do a big rewrite.
lead: We decided to rewrite our entire hosting platform. Here is more on the process and how we are doing so far.
figure:
  src: rewrite-poster.png
tag:
  - chronicles
---

A few years back, we faced a critical decision: iterate on our existing codebase or embark on a big bang rewrite. Common advice is to iterate:

> They did [...] the single worst strategic mistake that any software company can make: They decided to rewrite the code from scratch.
> -Joel Spolsky 2000 ([Things You Should Never Do](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/))

## A tough decision

We did not took it lightly. In fact, it was one of the reasons making my co-founder Oliver leave. I really do see the benefits of incremental updates: Ship features sooner, deal with a system that isn't perfect, but you know very well. Refactor, don't rewrite.

Yet, I think a rewrite is necessary for us: As [DHH phrased it](https://signalvnoise.com/posts/3856-the-big-rewrite-revisited), we need to **leap not skip** ahead to achieve our vision. We need to unburden ourselves from technical constraints and legacy compatibility concerns. The existing code base is too hard to maintain and extend. A new abstraction model is required.

## Halfway there

It's a very ambitious project and of course it takes much longer than anticipated. Rebuilding the entire platform while simultaneously improving it's feature set is a monumental task. There are many loose ends still. Every day new details emerge (unknown unknowns). I can see from first principle now why big rewrite projects fail.

> We are writing new bugs instead of fixing old ones.

It's recommended to put out a minimum viable product to gauge user interest and gather early feedback. But I feel our platform is the sum of all tightly interconnected parts and so I can not see what an MVP would look like for us. Despite a somehow sticky business model, the rewrite remains a very big gamble. This new platform needs to be the bedrock of our business for years to come.

## My take now

Experience breeds wisdom, and past mistakes make us cautious. Risk aversion increases with age. However, there's also a certain naiveté that can be advantageous when embarking on a daunting endeavor. As Mark Twain quipped:

> They did not know it was impossible, so they did it.

The road ahead is long and the finish line is not in sight yet. We have recently restructured our roadmap and postponed some goals. We are slowly approaching a closed alpha phase.

I am proud of our progress and what we have achieved so far and i'm incredibly fortunate to work with such a talented and dedicated team.
