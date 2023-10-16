---
author: fl
title: Migration help
excerpt: Helping existing users boarding the new dashboard.
created: 2015-02-26
tags:
  - chronicles
---

The new fortrabbit dashboard has finally landed. This [follow up](/new-dashboard-migration-guide) guide helps existing users to explore the new features and spot the differences fast.

## Keep calm and code on

**The migration is designed for hustle free upwards compatibly**. Nothing should be broken. Everything should work as before. However, we would like to encourage you to learn about the new features and workflows:

1. Update to new Company model.
2. Review if you have frozen Apps you might still need.
3. Review your code access.

Read on to learn about all the goodness.

## Humanized user account model

The old user model with fortrabbit V1 was flat like Twitter: Everything is an Account, you sign up with different Accounts, either personally or on behalf your company.

Now, with the new fortrabbit, the user model is more like Facebook: A User is always a human being, an organization is a Company, that can be owned by Users. This way you can better map your real world relationships onto fortrabbit and work better in a team.

* [Collaboration help](http://help.fortrabbit.com/collaboration)
* [Multi client model backgrounds](https://medium.com/@frank_laemmer/our-multi-client-model-3b965d2f1060)

## Kill instead of freeze

We changed user boarding from freemium to free trial. You can still try our service for free, but the procedure is different now:

* **No more waiting slots** — always get a free tial right away
* Start a trial Apps as often you want
* Only have one free trial App running at a time
* The official trial period is 72 hours
* You can ask us to extend that trial!
* Trial Apps will be terminated at the period end.

Of course everything is opt-in, you will not be upgraded to a paid.

* [Original announcement and backgrounds](/sunsetting-freemium/)


### Frozen legacy

You won't find your frozen Apps any more in the new Dashboard. That is hopefully not be a big deal as we know that 99.42% was for simple testing purposes only and you most likely have a local copy anyways.

**Is there a frozen Apps you still need? Act now!** We still have all the data backed up. Please [get in touch](https://dashboard.fortrabbit.com/support) so we can send you an archive with your App's data. We will finally delete all the old frozen free Apps by the end of April 2015.


## SSH keys on Account not App

We now store SSH keys with your Account. So whenever you get create a new App or get access to an existing one, your SSH key will be automatically installed. That makes managing code access much easier. We recommend to migrate the keys currently stored with your Apps into your Account.

Of course: All previously installed SSH keys are still stored with the App as they were before, so nothing breaks. You can still add App-only SSH keys, since there are use-cases like external continuous integration provider which still make sense.

* [About code accesss](http://help.fortrabbit.com/code-access)

Also, we finally allow SSH key authentication with your App's SSH account. Previously this was only possible with your App's Git repository. Again, to make sure we break nothing: all existing Apps have still password authentication enabled. You are free to switch to SSH key only or activate both or stick with passwords. New Apps will default to SSH key only; both for Git and your App's SSH account.

## New structure, same total price

We have renamed and restructured our product palette. Many of the refactoring was due to upcoming services. Your invoice will contain differently named items , but at the end of the day: the total price will be exactly the same in all cases and setups.

### Long invoices in the first month

In the month of the switch (old Dashboard > new Dashboard) your invoices will be double as long as usual. That is because you have partly used the old products and are now partly using the new product structure. Again: the total sum will not change. So don't worry about it.

## Billing changes

We have also integrated our own invoicing solution.

The most notable change is that you can now have **multiple Billing Contacts** associated to your Company (not the Account). Sounds complicated? It's not, it's pretty much like with Amazon, where you can also manage multiple your delivery addresses and billing methods. And if you only need one billing contact, you won't even notice it.

* Invoices are beautiful HTML pages now
* A new invoice archive to view and download archived invoices
* Invoices are now dated at the end of the service period month (that already happened with the last invoice from 2014)
* You'll be notified if a payment has bounced


* [Billing & accounting FAQ](http://help.fortrabbit.com/billing)


### EU B2C MOSS tax law implementation

If you're not living in the EU then you can safely skip this part.

We had to adapt the new [messy](http://techcrunch.com/2014/11/25/eus-new-vatmoss-rules-could-create-a-vatmess-for-startups/) EU tax regulation changes. This potentially changes for you:

We only can assume that we have a professional B2B relation with you, when you supply us with your validated and verified VAT IN. Please do so, it's less stress and you don't need to pay Value Added Tax upfront. Special case: businesses from Germany, they always need to pay VAT upfront.

Otherwise (no VAT IN given) we need to assume that we have a B2C relation (you use our service privately as an end user). In this case we'll add your local VAT rate on all invoices.



## Other new features

* **New [professional support model](http://www.fortrabbit.com/support)**
* Minimal design unifying all properties
* Completely rewritten up-to-date [help pages](http://help.fortrabbit.com)
* New marketing website [marketing](http://www.fortrabbit.com)
* Newly designed [blog](http://blog.fortrabbit.com)
* Enhanced mobile friendliness
* Activties are nicer now > old activties are marked with `(legacy)`


## Please reply

That's a major update for us. We hope you like it. [Feedback](https://dashboard.fortrabbit.com/support) is highly welcome!
