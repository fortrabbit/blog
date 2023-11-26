---
title: New dashboard migration guide
author: fl
excerpt: Learn what is going to change with the new dashboard.
created: 2014-10-15
tag:
  - chronicles
---

# Boarding the new dashboard

**tl;dr** The new dashboard is coming. It's going to be phpantastic. No action required from your side (most likely). Our [last article](/mission-statement-the-new-dashboard/) praised the new features this article explains changes.

## Freemium to free trial

**DISCLAIMER**: Don't be scared. We are (still) the good guys. This is not a shady subscription trap. Everything is opt-in. You can cancel at any time. You will not have to pay a cent more.

We are finally going to fix this free App slot thing; those nasty freezes. As [announced](/sunsetting-freemium/) we are going to introduce a timely limited free offer instead of a free-forever model. You can still create free test/trial Apps to evaluate our service. Free test Apps will now be removed (killed) — not frozen — when their time is up. You can always start a test/trial App: No more waiting slots! The testing period is (most likely) 72 hours, but you can ask us to extend it as long as you think you’ll need. Here is what happens when we switch: Your running free Apps will be automagically converted to trial Apps. Your already frozen (free) Apps will no longer be available. Yes, wee are going to delete tens of thousands of neglected "you have arrived" test Apps. 

#### How to backup currently frozen Apps

Do you have any frozen App that is important to you? Make sure you grab everything now. 

  1. **See it again**: unfreeze your App in the dashboard
  2. **Get code**: since you are using Git (you are, aren't you?): you most likely have a local copy of the code already. If not login via SSH/SFTP and download or git pull everything
  3. **Get database**: if you have a MySQL database, connect to the database (via SSH tunnel) and export the database

## Git/SSH/SFTP workflow changes

Managing your public SSH keys for Git & SSH access becomes less of a pain: After the switch, you can manage your SSH keys centrally — with your Account.. and they'll be added to all the Apps you have access to. Also the keys will be installed to your all your Apps' SSH/SFTP accounts as well (though all manually installed SSH keys will be kept as well). Of course, App-only SSH keys will still be possible, so you can safely integrate with 3rd party services which you don't want to grant access to everything you own. During the migration we will do our best to your SSH key to your Account. But better safe than sorry: If we cannot definitely associate an SSH key with an Account, we will keep it as App-only. So no Git/SSH/SFTP accesses will be added nor removed. As for password authentication for SSH/SFTP: Still possible and all existing passwords will be kept. However, you can now switch it off (which is the default for new Apps) at any time. Keep in mind: Our new Git-mostly "Ephemeral Apps" are also going to come soon (and they are going to be great). 

## Teamwork changes

We are revamping our "permission management". It’s going to be lovely. I have written about the backgrounds of the new multi client model [here](https://medium.com/@frank_laemmer/our-multi-client-model-3b965d2f1060). So how will it look? There are going to be "Owners" and "Admins". These will grant you access to a Company, which in turn owns Apps which you then can access. Also there will be a "Developer" role (which also belongs to a Company): it grants you access to only a subset of the Apps of a Company. Sounds a bit complicated? Nah. "Progressive disclosure" will help, you will find all the advanced features when you need them. This happens after the switch: The "Analyst" role (let's say: sparsely used) will be removed. We will convert the current "Junior Developer", "Lead Developer" and "Project Manager" to the new "Developer" role and grant them access to all the Apps they can access right now. This implies some downgrades: "Developers" cannot scale nor remove an App. 

## Product structure changes

The new structure will be more modular and will smooth the way for the upcoming Ephemeral Apps. Here is how it goes: We are splitting the current App into three separate products: The App (a base container, if you will), the scalable PHP product and a scalable MySQL product. Don't panic: The price is going to be exactly the same. The great thing about it: It will allow us to offer far cheaper Apps in the future. On that note: we are also changing our whole invoicing system. You will have an invoice archive where you can download previous invoices and suchlike. 

## Only CNAME routed domains

Your old naked domain routing A-Records will still work. But we will not communicate A-Record IP addresses routing any more. Naked domains are visually more appealing and easier to set up, but they come with huge disadvantage that we can’t move your App quickly in case of emergency. We already stopped communicating A-Record endpoints. 

## Timeline

It’s going to be ready when it’s ready. We hopefully will switch happen later this year, November or **December**. 

### The switch

We’ll expect a little downtime for our dashboard during switch. As far as we see now, your Apps will not be affected. Maybe the invoices will be delayed. 

### Communication

We gathered all changes here. We will update this page when, something else will come up. You will be informed about the exact date at least a week beforehand.