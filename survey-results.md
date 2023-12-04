---
author: fl
created: 2015-05-12
title: Survey results
intro: What our users are saying and what we think it means.
tag:
  - webdev
---

## Thanks for your answers!

We have just asked you a few questions about our service and hosting in general. Everybody hates surveys. But it's important for us to get to know you a little better. It helps us shaping the future fortrabbit. Here is what we have learned and what not:

## Results

<iframe src="https://fortrabbit.typeform.com/report/McsJu6/ttaq" frameborder="0" class="spacertop" style="width:100%; height: 500px; border: 1px solid #6C5F53"></iframe>

Just in case you wonder: most question allowed multiple choices, that's why some totals are more than 100%.

### Get the word out on Twitter

We asked our Twitter followers to take the survey. We "reached" around 1,700 PHPeople and got around ~30 answers from that. Ok.

### E-mail marketing

We also did an email campaign to 13,000 of our users. It had an  open rate of 25%. We got around ~180 answers from that. Learning: A newsletter is a reliable way to get answers in. But around 200 mails for 1 answered survey is a lot of waste.


## Asking the right questions is hard

We have discussed the questions internally before publishing of course. My personal premise:

> The way you ask the question is much about the answers you will get.

We are especially looking for indicators on a new pricing strategy. So we have asked what is more important, "price" or "quality of service"? You could answer with a range-slider from 1 to 10.

The average answer, as you could guess: **5.57**. Of course everybody wants to have perfectly-balanced price-value. I would like to rephrase the question like this: 

**Which hosting package would you buy?**

1. 99% uptime guarantee for 5 €
2. 99.9% uptime guarantee for 50 €
3. 99.99% uptime guarantee for 500 €

I guess not everybody would take the good balance. But what, if we phrased it like that:

**Which hosting package would you buy for 5 €?**

1. supreme performance, but not guaranteed availability
2. average performance and alright availability
3. rather low performance, but very high availability

Those 5.57 can go both ways. Our take: People are aware that cheap comes not free.

## We got contradictory signals

We already knew that people value speed as an important indicator for choosing their hosting provider.

The background: Currently our free trial is our smallest plan. We are now considering a new trial which comes with far bigger resources, so that the actual performance can be experienced. The problem with starting on a small plan is that you might not get what's possible. 

I personally believed that performance bottlenecks will mostly be found in production, after you already moved your application to your provider. Checking out the speed of a new web host is tedious - I figure really few would actually do it. On our platform we are seeing most people using the trial App to check out the deployment and run a simple `hello world`. So we asked the questions:

**1. How do you measure the speed of your new web host?** So it turns out that most of you PHPeople do test the speed.

**2. How fast is fortrabbit?** Well, most of you didn't test it - which contradicts the previous result and left us non the wiser. 


## Interpreting the answers is hard

Now what does the above teaches us? I would argue that if we have phrased the first question differently, we would have become different answers — "Do you test the performance" instead of "How do you test performance". I think the second answer is the real one — people don't test hosting provider performance upfront. 

You could also argue that not everybody is a fortrabbit client (yet), so that's why they haven't tested the speed yet. Or you could argue that people want to test the speed - but don't.


## Geo-prejudices

As a company we need to be oriented on profit. Being based in Europe, it's not surprising that we make most revenue with clients from northern Europe. Also, maybe a bit surprising, is that there is indeed a a lot of interest in our service from Asia. Our general assumption was: In lower-income countries our pricing is a bigger issue. To confirm this we geo-tagged the survey. Learnings:

About 10% asked for a more affordable pricing structure. As it turns out, they came evenly distributed from Asia and Europe/US.

About 5% asked for "free hosting". Here the majority came from Asia. Of course we are not going back to that (again): It simply does not work. 


## Other learnings

The last question was "What are you missing at fortrabbit?". Again, we wanted to check out if we are on the right track or if we are missing any trends. Most answers are very individual, feature X, feature Y, feature Z. Too many features making us too flexible and versatility are hard to tackle with our small team. But we are aware.

The Bitbucket integration request was repeated. Why Bitbucket and not GitHub? Bitbucket offers private repos for free ;)


## Notable feedback

> Somebody to proof read your documentation. More transparency about the actual app and what you get. A CLI. An API.

Thanks again to everyone!

<!--

"Its pretty good, but I still spin up my own vpses for stuff and save money over long term as I work on loads of smaller websites, so simply using vps with ispconfig 2 does the job. For larger apps I also set up a vps myself, as it only takes a few hours using scripts etc. In other words fortrabbit looks cool, but I don't see the need to pay the extra as I can just use vpses with the help of ci tools and stuff like Laravel Envoyer and Forge. Turns out to be really cheap and flexible solution."
-->