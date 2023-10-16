---
author: fl
created: 2018-04-16
published: true
title: fortrabbit is GDPR ready
excerpt: GDPR is here. Wat is changing for our clients, what not, why and when.
lead: Comply by the end of May. The General Data Protection Regulation is coming. This post reflects when, why, what and what not is changing for our clients.
image: gdpr-ready-poster.jpg
tag:
  - chronicles
---

TLDR; No action required for for our clients, we are all good. You have some online business? Keep reading, as these changes might affect you as well. DISCLAIMER: This is not a legal advice. This is just our "worst practice".

## Does GDPR apply to me?

Yes, you have to keep GDPR in mind, when your online business is based in Europe, or you do business with Europeans. GDPR spans B2B and B2C relations.

## Why is GDPR so good?

It is strengthening the security and protection of personal data. That in general is a very good thing.

## Why is GDPR so bad?

Just like with other EU laws — hello MOSS — the motives are noble, but the actual technical implementation is to many degrees unclear. For small and specialized businesses — like ours — some rules might be hard to come by with and even be contra-productive.

## Opt-in instead of opt-out

Now, for the sake of simplicity, a general rule of thumbs is that everything needs to have an explicit opt-in, instead of a general opt-out.

### Sign-up double opt-in

With e-mail double opt-in, a new user first needs to verify their e-mail address before completing the sign-up process. This is a very common practice. So, when signing up to a new service, you first need to check your mail, and click the link to continue.

We have a "quick boarding" feature, where users can try out our service right away. The double-opt-in (confirm your e-mail) gets send, while signing up, but, even without clicking the link, the user already has access to the Dashboard to play around and test it. To fully activate the Account, the link in the welcome mail still needs to be clicked.

This is not changing, as we believe that we still comply this way and that the delayed double opt-in is a usability win, while still respecting security and privacy.

### E-mail communication opt-in

New sign-ups here are also getting subscribed to e-mail communications:

#### Transactional mails

These are all mails send by the system, some by user interaction, some by time intervals. Common examples are: The before mentioned e-mail opt-in, a forgotten password link, the monthly invoice, the notification that a new collaborator has joined a Company, a reminder that a trial is about expire.

Some of those mails are required by law or to make the service fully functional. Others might be marked as "retention" or even "marketing". For the "Trial App ends soon reminder" e-mail, some clients asked us to opt-out or even better opt-in on this.

We have considered that carefully and deactivated all transactional e-mails with purpose to keep users engaged. We have compared our service with other similar ones and came to the conclusion, that we are sending very little mail to keep users engaged. On the other hand we get regular "Nobody told me." complains on deleted trial Apps. Yes, we did, with these transactional mails.

So this is not going to change now. We are looking into ways to further differentiate here in the future.

#### Newsletter

Well, how do you define newsletter? Yes, newsletters can get spammy. Our "newsletters" are coming on a very sporadic level (6 newsletters in 2017 ) and they contain quality content that is even sometimes crucial for client communication. Our newsletter informs our clients about important service changes — think: new service features, changes to the TOC and PHP and stack deadlines.

There are already options within the Dashboard Account Notifications settings to easily opt-out, as well as a one-click opt-out link in the newsletter.

How we have changed this: When signing up, there is a box, that the user agrees to be contact by e-mail by us. This includes transactional mails, possibly downtime communication and newsletters. This checkbox will be required to sign up.

### Terms and privacy opt-in

With GDRP, it is now required to actively opt-in to the terms and privacy when signing up. So something like: "By clicking the button above you'll agree to our TOC" is no longer allowed.

When signing up, there now is a checkbox, that needs to be clicked.

- - -

#### Signup form before GDPR

![](/dist/img/before-gdpr.gif)

#### Signup form after GDPR

![](/dist/img/after-gdpr.gif)

- - -

## Export and see my data

With GDPR, there should be a possibility for the user to download all data. Ideally, that should be available in the Dashboard.

Well, I think that makes sense for social networks or any service, where content is generated. Personally, I will be happy to be able to download my posts from Medium. But I hardly can imagine any case this would make sense in a web hosting control panel. Also let's talk about the implementation here, the format for such a download is not defined, so what should a user do with some custom `.xml`, `.yml` or `.json`  or `.sql` file?

So, this is not going to change here now. It is not required that there is a button for this, so we reserve the right to make this available on support request.

## Forget me

The right to be forgotten is also quite a good idea. So, with GDPR in place, the Account deletion, either by client or by us, should actually be: Delete all data; Remove all the clients data from third party services; Remove all backups. Let's have a look:

### Delete all data

Well, kind of. It depends. When there is a single Account / Company with some Apps, this mostly applies. All data is getting erased. Expect: for what we need to need to keep for book keeping  — 10 years required by law.

From a technical point of view, mind that we are in fact deleting all the files of your Apps, all your databases and all database entries with us, but we are not overwriting them with gibberish text seven times. That means that forensic procedures might bring back some of the data.

When collaborating with others here: The Account gets deleted, but Company, Billing Contact and Apps might stay there, as there might be other Owners around. We are printing a big yellow warning page on this already.

Also, we might have contact via personal e-mail with your clients. We are required by law to keep all business communication for 10 years. We can not delete the e-mails you have sent us and also not the mails we have sent you. We are using Google gSuite for e-mail hosting, so when you write us an e-mail, that is and will be stored there.

Nothing changes, I think we are good here.

### Remove data from all third party services

So when a client deletes their Account, all external services should be notified to also delete anything related. Let's have a look at what we have in place here:

* Intercom support channel — YES, Associated IDs will be deleted when deleting the Account
* Credit Card processing — NO, we have to keep billing related data required by law for ten years. The actual credit card details are not stored with us anyways.
* Google Analytics and other tracking — YES, as we don't associate our Accounts with user journeys.
* Mailchimp newsletter — YES, when you delete your Account, you will be unsubscribed from all newsletters
* Statuspage updates — YES, if any.
* Additional copies of user data in staging environments — Does not apply.
* Postmark App — YES

### Remove Backups

When Apps get deleted while deleting Accounts, possible available Backups (when booked with a App plan) will stay around until the retention period is over. So those backups are not getting deleted immediately.

We believe that immediate deletion is not in the interest of our clients. We have support cases, where clients accidentally deleted their Apps or even Accounts and are quite happy about provided backups. Also, from a technical point of view, most of those delete actions will be carried out by some kind queue/worker task, so this can't be done on the fly.

Nothing is going to change here. Possible available backups will get fully deleted when the retention period ends.

## Restrict processing

When an Account is visible to other Accounts, itself should have an option to hide its identity. That totally makes sense for social networks and alike, but in a B2B hosting solution with collaboration features, transparency means security. People making use of our team work features need to know about each other. Would you give code access to a mysterious: "This user prefers to make a secret about himself"?

This is not going to change. Other members in your fortrabbit collaboration team will be able to see your: name, e-mail address, avatar and Dashboard history.

## Check 3rd party services to be compliant

Yes, as far as we know, for our business everyone is.

## Updated privacy pages

Yes, we did a while ago and we have noticed you before. There is a [third party transparency report](https://www.fortrabbit.com/privacy#third-party-services).

## Further readings

Oh boy. GDPR is a huge topic in the SEO scene, you'll find thousands of shady copy/pasted articles. But this is a good one:

* [GDPR - the practical guide](https://techblog.bozho.net/gdpr-practical-guide-developers/)
