---
title: Sunsetting a few features
author: fl
excerpt: The SMTP Wrapper and the ReSync Tool will go away.
figure:
  src: move-fast.jpg
created: 2014-06-18
tag:
  - chronicles
---


Our [new dashboard](http://fortrabbit.com/feature/enhanced-dashboard) is in the making. There are going to be lot's of cool new features, but we also plan to skip some _not-much-used-not-so-good-not-so-future-proof_ ones for the first time. Here is what's going to happen and bit of **end of life philosophy**.

**tl;dr** We are planning to **disable** our **[SMTP Wrapper](http://fortrabbit.com/docs/how-to/php/sendmail#smtp-wrapper)** (sendmail proxy) and the **[Resync Tool](http://fortrabbit.com/docs/essentials/deployment-workflows/resync-tool)** (Git/Webspace helper tool) by the **31st of August** 2014\. Please speak up now if you don't want that. 

## Alte Zöpfe abschneiden

The headline above is a German idiom and can be translated to: "cut of old pigtails" and means something like to get rid of old habits. Web hosting is a business that profits from your forgetfulness. Ask yourself: How many of your old websites are still running — PHP5.3 or lower? Yes on the one hand the hosting service should be as stable as a rock, backward compatible forever. On the other hand, we all want to get that new technology that came out last week in our hands, as soon as possible. Is it possible to run a managed cloud hosting platform that is future- and backward-compatible at the same time? It's not, so we need to find a good balance between accretion and erosion. Facebook moves fast <del>and breaks things</del> [with a stable infrastructure](http://www.cnet.com/news/zuckerberg-move-fast-and-break-things-isnt-how-we-operate-anymore/). Apple made their Mac operating system freely available so that people adapt the latest version faster. Major browsers get an automatic update every month, so you don't know the version number anymore. And even the Internet Explorer has a dev channel these days. Everyone is on a rapid release cycle now. So are we. We subscribed to progress. We encourage you to move with us. We want active and happy clients. We will communicate upfront with enough time ahead and clearly about changes. We will answer your questions, help you with migration, name alternatives and listen to your feedback. Of course we will also the platform stable, reliable, predictable and stable. We support the playful hacker in you, while respecting the business owner needs. 

### About the SMTP Wrapper end-of-life

Our SMTP-wrapper is a proprietary little helper tool to use the popular PHP [mail()](http://www.php.net/manual/en/function.mail.php) function on our platform. The background is, that just plain mail() probably won't work from the AWS network. In the **current implementation** you can enter SMTP access credentials in our dashboard to use mail(). We then will catch the mails from mail() within your Apps code and deliver them via SMTP. We are **skipping this feature, because** it's mostly for the benefit of novice users and we think you are more advanced. Also there were lot's of misunderstandings and problems setting it up. It is also not much used and there are good alternatives. **What you need to change** when you are using it: For Laravel or some other framework that abstracts mail sending: Use SMTP directly from the framework itself — that's a much cleaner solution. For Wordpress: there are plenty plugins to setup and easily use SMTP instead of mail — easy. For the sophisticated heavy user: Consider to use Transactional mails as a Service (like PostmarkApp, Mandrill, SendGrid …) — benefit from the benefits. Please change your code if needed until 2014-08-30, or raise your voice now. 

### About the ReSync Tool end-of-life

Our [Resync tool](http://fortrabbit.com/docs/essentials/deployment-workflows/resync-tool) is a proprietary deployment helper tool to get your Git and your webspace into sync (after you messed up). The usual use case is, when you used the update button in WordPress and then suddenly the code on the server is newer then your local one. And since web space and remote git repo are not the same, you can not just pull these changes back in. We are **skipping this feature, because** it's not needed for our upcoming ephemeral (12-factor) Apps, it's a source of misunderstandings, it's not much used, it's a hack to compensate for bad practice and there are alternatives. **What you need to change** when you are using it: Don't mess up: plan carefully, use composer and Git and best practices. Our [deployment file](http://fortrabbit.com/docs/in-depth/deployment-file) is an alternative for syncing your local stuff up to the remote webspace. Please change your habits until 2014-08-30, or raise your voice now. 

### BTW: About PHP versions

We will incorporate new PHP versions as soon as we can. We will support old versions as long as there will we be security fixes for it. PHP 5.3 will be due within the next months (though we don't support it anyway). Given PHP's record, 5.4 will probably become unsupported sometime during mid 2016 , that's 2.5 years ahead. What do you think? What are your expectations?