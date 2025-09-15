---
title: Action-oriented UX
author: fl
created: 2024-07-24
intro: Verbs first for interfaces with more natural language.
lead: This is usability experience concept. Verb first interfaces to be closer to natural language and human thinking.
figure:
  src: action-ui-poster.png
tag:
  - opinion
---

## Object-oriented UX

Before explaining my new idea, let's first see how objects and actions usually correlate in UI systems. See this screenshot from the Stripe dashboard:

![Stripe dashboard](/images/stripe-object-ui-annotated.png)

I claim: Many user interfaces follow an object-oriented approach. We see lists of objects (items), and by clicking on them, details and possible actions are revealed. This interaction prioritizes the object (the noun) over the action (the verb). This is fine and people are used to it.

## Action-oriented UX

Offer an additional verb-oriented entry point:

![Manage landing page](/images/action-ui.png)

The screenshot shows available tasks grouped by action. This is an early dummy of our new dashboard (in the making). It juggles multiple object types and serves as the hub for managing collaboration settings. This aims to enhance at-a-glance comprehension of available actions.

### Routes

With action oriented UI we can build different kind of routes (endpoints).

A user wants to delete an app:

- object-oriented: `/apps/ap-1234/delete`
- action-oriented: `/delete/app?ap-2134`

A user wants to create an app:

- object-oriented: `/apps/create`
- action-oriented: `/create/app`

The action based URLs look better to me, than the object based URLs. They translate better into English language and it least to how I think about systems.

### Relations

Editing a relation of two objects can be approached from three sides now. To edit the team-developer relation, a user can start the task in an objected oriented style from the team page by selecting a developer or they can visit the developers page to select a team to proceed.

Now with action oriented UX they can also **edit** the relation of these two objects in the first place — start with the action. 'Edit a team developer relation'. This opens a multi-step form. A user selects the developer first, to then edit the roles in teams they are part of. Or the user starts with the team first, then chooses a developer to edit their role.

![Multi-step form](/images/multi-step-relation-forms-annotated.png)

Now back to the routes. In action oriented UX the final step can have this pattern:

- `/edit/team-developer?tm-324&pe-1234`

`tm-123` define the team object and `pe-1234` the person (developer). With these two parameters, this step can also directly linked from the objects.

### CRUD actions only?

So far I have explored to apply this pattern for primary actions on objects only. It could potentially also be applied to any kind of additional configurable parameter of objects. A user may want to **change the PHP version** of an environment. With object oriented UX, the user needs to find that setting with the environment. Imagine a search box or command bar where you just type php version to start the process. Next you can an environments from a list.

## We may not ship it

To launch a first version of our [new platform](https://new.fortrabbit.com) (hopefully this year) we need to prioritize features. Many good ideas need to be deferred to later releases or even dropped. In this case, the odds are:

- It's a lot of work to maintain different entry points to do the same thing.
- There are some quirks with flows that don't really fit in the pattern well.
- All these options might be confusing. I haven't noticed this concept anywhere else.

## Addendum

Of course, only after writing these words, I did a web search on the topic. It seems that Object-oriented UX is indeed a thing, mostly owned by Sophia V. Prater. There is even an acronym: "OOUX" - [www.ooux.com](https://www.ooux.com/) - concepts go much deeper than my lazy sketch above. Yet, my invention now also has an acronym: "AOUX".
