---

title:    Multi stage deployment
author:   uk
excerpt: "How to setup a production/development work-flow for website development."
created:  2012/10/01 10:18:25

---

UPDATE 2021: There is also a new [help page](https://help.fortrabbit.com/multi-staging).

This article targets new developers and developers which never had the chance working with multi versioned websites before. If this fit's you: Read it. Staging is a good tool in your belt you won't regret to know.

## What staging is all about

Staging has many [meanings](http://en.wikipedia.org/wiki/Staging), I will focus only on those in the context of website development. Wikipedia [defines](http://en.wikipedia.org/wiki/Staging_%28websites%29) a staging site as a website used to assemble, test and review its newer versions before it is moved into production. To put it in other words: You've installed your website on two different places (aka deployments or environments). One installation is called **production** (or sometimes _live_) : This is your live website. Users are visiting it and interact with it. The other installation is called **staging**: You, your co-developers, authors and whatnot using it to prepare and test stuff which is to be released into production. In short: you do not perform open-heart surgery by coding directly on the production website. Other keywords in the context might be: "App live cycle management", "one codebase many deploys". 

## Multi staging / multi level deployments

Depending on the size of your project, sometimes you need more deployments. It's best explained with use cases. 

### Purpose separation

The bigger the team working on the site, the more specialized each member tends to become. There are designers, editors, programmers, controllers - you name it. If you've worked / are working in a team of more than two people, surely you have experienced the following: The coders are working on the (non production) site. Something breaks temporarily. The programmers know, that this is temporarily, the designers, authors and everybody else do not. So they either file bug reports, which annoys the programmers, or they stop working, which wastes time. Both is bad: It breeds bad temper and costs time and money. Thats why, as soon as the team size warrants it, there should be more deployments - at least one for each team. However, keep in mind that the structure / amount of the deployments should be designed based on the needs and conditions of your project. Do not put more levels in than you can handle. [Here](http://en.wikipedia.org/wiki/Development_environment_%28software_development_process%29) is the general definition of development environments from Wikipedia. 

### Example: Three level deployment

This one I've used quite a lot. It works good with a team of three or more. 

  * **Development**: A space for coders where they can break things without being afraid of complains by the rest.
  * **Staging**: Where new code, which is finished (aside from bug fixing), can be deployed so everybody can review/test it before it is released. Also less destructive implementations (eg CSS changes) can be done.
  * **Production**: The live website - no bugs nor half-backed content here (hopefully).

### Example: Four level deployment

If the team gets bigger and there is money for dedicated testers: 

  * **Development**: A space for coders where they can break things without being afraid of complains by the rest.
  * **Testing**: Designated testers review the updates made in development. Test suites are run.
  * **Staging**: Only final review is done, no active development.
  * **Production**: The live website - no bugs nor half-backed content here (hopefully).

### Feature development

When deployments are easy to setup, it lend itself to outsource feature developments in dedicated environments. The bigger the new feature and the more core changes it requires the more should you consider this. Also sometimes you want to try out some bigger changes, which might not ever make it to production (if they fail to to what you want). Either way, feature deployments make sense, because they to not interfere with the regular development or (even more important) bug fixing. If you are in the middle of a core changing feature which is weeks away from being stable, really don't want to push it online, just because you need to fix a critical bug. 

### Right separation

Most [content management systems](http://en.wikipedia.org/wiki/Content_management_system) implement already a kind of right separation: An author/editor is allowed to write an article but only the executive editor can publish it. However, in the context of code development, this is not the case. Assume you are the CTO of a company and hire two new coders. You might not want them to to publish code into production, as you don't know judge their skill level or some company policy prohibits you to do so. So taking the four level model from _Purpose separation_ above, the new guys can only access the development deployment, whereas more senior staff is allowed to publish into staging. You alone are responsible for the live environment - so you alone can publish onto it. 

## The data synchronization problem

Runtime data, such as images uploaded by users, database rows generated by user interaction and so on, is the most difficult problem to solve in multi level deployments. General there are two possibilities: Your data is shared or it is not. In development and/or testing deployments, you really can mess up the whole system. What you want here is data separation: different database, cache and file storage. What you want is a simple one way synchronization (production -> development), so you can rebuild your destroyed development very fast. Normally it is not required to have live data, so using the last night backup as base for this is a good idea. In staging or authoring levels, it is sometimes necessary to use exactly the same data as in production. Still, try not to do this - or at least be aware what you are doing. 

## Downside of multiple environments

Yes, there are some. The impact is in general greater, the more you overreach in the amount of deployments you really need vs the amount of deployments you have. 

### Delay

Multi stage environments delay the deployment of a particular line of code as they have to pass multiple levels. Depending on how strict you enforce them, it can take days until a simple wording change is published. This can yield bad behavior, eg that minor (deemed) changes are dropped completely. The time delays and omitted changes will cost you money and can reduce the overall quality of your application. The solution for this strongly depends on your (company's) policies and the possible impacts (money loss) if you'd relax those. 

### Complexity

> Make everything as simple as possible, but not simpler. Albert Einstein

Having multiple environments adds additional levels of complexity. You can make new mistakes based on the different infrastructures your app is in. Same as above: Don't over-egg the pudding. 

## Bottom line

Staging is a tool as any other: Use it with care. Do not overdo, but also do not downplay it's need / purpose to the last minute. In my opinion, you should at least plan ahead for multi level deployment. Implement application level recognition of the deployment early on (in a sense `if in_staging: use staging database; else: use production database`). 

## A great proposal: Git flow

In the context of modern web development and deployment, you should probably know about the [Git flow](https://github.com/nvie/gitflow) Git extensions, which are based on the proposal of a [successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/). At this time, Git flow does not address deployment at all, but it's proposed branching model gives you a good structure to start on.