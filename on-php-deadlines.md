---
title: On upcoming PHP deadlines
created: 2018-09-06
author: fl
intro: 'PHP 5.6 and PHP 7.0 deadlines: Why is so much old PHP around? What we will do!'
figure:
  src: php56-deadline-poster.jpg
tag:
  - opinion
head:
  meta:
    - name: 'keywords'
      content: 'deprecation, EOL, php5.6, php7.0, php7.2'
---

<p class="type-l">
  <span id="timer">
    Only <span class="type-bold marked"><span id="diff-days"></span> days</span> until the end of live for PHP 5.6 and PHP 7.0.
  </span>
  <span id="time-over" class="hidden type-bold marked">
    PHP 5.6 and PHP 7.0 are not supported any more.
  </span>
  Why update? Why is there so much old PHP out there? How to establish an up-to-date mindset.
</p>

<script>
  var oneDay = 24*60*60*1000;
  var eolDate = new Date(2018,11,31); // 11 = December
  var todayDate = new Date();
  var diffDays = Math.round(Math.abs((eolDate.getTime() - todayDate.getTime())/(oneDay)));
  var elem = document.getElementById('diff-days');
  elem.innerHTML=diffDays;
  console.log(todayDate);
  console.log(eolDate);
  if (eolDate < todayDate) {
    document.getElementById('timer').classList.add('hidden');
    document.getElementById('time-over').classList.remove('hidden');
  }
</script>

This is part one of a series on the approaching end of life of PHP 5.6 and PHP 7.0. This is the long read, the general theoretical part including details and philosophical questions. In the next parts more actionable instructions on how to actually migrate, especially for fortrabbit clients will be included.

As time flies by. Only three years ago, we announced that [PHP 5.6 is becoming the new default](/php-upgrade-path-5-4-5-6-7-0). Now, we are already facing the end of that and even the ascendant version 7.0 .

## Why upgrade to PHP 7.2 anyway?

**It's about time.** "PHP 5.6" is the last 5 version around and there will be no security patches from December 2018 on. Any new vulnerabilities will not get fixed any more. The same applies to the initial PHP 7 release, version 7.0. It was released in December 2015. The current version is PHP 7.2 and PHP 7.3 is approaching next.

![php deadlines approaching](/images/php-version-deadline-on-php-net.png)

See the [officially supported PHP versions and there lifespans here](http://php.net/supported-versions.php).

### How much old PHP is still around?

![php usage according to w3techs](/images/php-usage-according-to-w3techs.png)

As of August 2018: PHP 5 is still the most used version of PHP. According on who you are asking, you will get different answers:

- **~80% old PHP** according to [W3Techs](https://w3techs.com/technologies/details/pl-php/all/all) (PHP 7 also includes the deprecated PHP 7.0)
- **~66% old PHP** according to [WordPress](https://wordpress.org/about/stats/)
- **~21% old PHP** according to [Composer](https://seld.be/notes/php-versions-stats-2018-1-edition)

Why the differences? Well, I believe **W3Tech** is just crawling the web sniffing the `X-Powered-By` header to get the version in use today. That includes all the public IPs with all the neglected websites out there. As this gives potential hackers information about the PHP version, it's common practice to suppress or fake this header, so maybe take this number with an extra grain of salt. **WordPress** is luckily a little ahead, as it is an active community of "web designers", with a big stake in the United States. And of course, Jordi with **Composer** is ahead, as those PHPeople are mostly "web developers" who care more about such things.

### Who is to blame for all the old PHP?

We started fortrabbit, around 5 years ago, because we were thrilled by the new PHProfessionality. Composer, Laravel — for us PHP really made the switch to a modern programming language. Still PHP has a bad rep for being the Pretty Home Pages language — and that is also still true. PHP was and still is (beside JavaScript) the first web native language to pick to create home pages. And many of those websites are still around. It's all those tiny businesses and their **semi professional web designers**. When you receive $200 to build a website for a restaurant, you are not likely to maintain it for the next 10 years.

And it's the **mass of shady shared hosting providers** who are keeping the clients locked-in in long term contracts and outdated versions. I can imagine that half of those PHP 5.6 websites could actually be switched off by now. But that's not the interest of the hosting providers, they are more interested in keeping them around.

### Our conflict of interests

It's tricky. Even here — with PHP cloud hosting fortrabbit — around a quarter of Apps are still running on PHP 7.0 and PHP 5.6. Luckily it's more PHP 7.0 and less PHP 5.6 which will make the transition less painful. Still it's a few hundred Apps and that's some good revenue for us. Most of those Apps are old of course, they have a life time of at least 14 months and sometimes even much or more. So those Apps are already older than the average App here — more likely to churn soon. We expect to find lot's of neglected projects their owners forgot about in there. Now, when we will start to inform the owners about upcoming changes, chances are that many of those projects will just be killed. Either the projects are not needed, or there will be no budget for migration efforts. PHPeople will be like:

> "Oh, that shit is still around? I need to take care of this now? Oh, and I haven't integrated those GDPR changes. I can cancel this right away. Cool! Let's do this instead."

We will loose a good number of Apps. As a business that's of course not in our interest.

### Or shall we keep all the old PHP?

We have discussed ways to deal with the situation. One idea was to keep those Apps still around, on unsecured PHP versions. Our fellow colleagues over at Platform.sh are following such an approach: Asking to upgrade but still keeping Apps on old PHP versions around - see [their blog post](https://platform.sh/blog/its-july-2018-do-you-know-what-your-php-is). The argument here is, that we should support the clients preferences as much as we can. This is technically possible here as well. We could accept the risk of someone leveraging not fixed vulnerabilities to break in, only causing some local damage. **But NO, we won't do that!** Still this could cause our IP ranges or App URLs to be down-ranked or included into SPAM blacklists. We also want our client base to be fresh, agile and alive.

### What to do about all the old PHP?

What ever the real number of old PHP installations in the whole internet will be, there soon will be tens of thousands of outdated and unprotected PHP servers out there waiting for hackers to take them over. Maybe we should all gather together and raise awareness for the situation so that more PHPeople wake up and update? What about a hashtag like **`#uPHPgraded`**?

Or maybe, even better, that's a call to establish new business models? Imagine, what would you do with that army of zombie servers? Bitcoin mining or even making Obama president again?

<h2 id="establish-an-up-to-date-mindset">Establish an up-to-date mindset!</h2>

Keeping your own code and the underlying software dependencies up-to-date is more than just a good practice, it's a requirement. On fortrabbit, we are in this together. We are responsible keeping the infra up-to-date; your are responsible for the code you write and use. Updating keeps your code secure, fast and agile. Our clients are obligated to use up-to-date software by [our terms under 4.13](https://github.com/fortrabbit/legal/blob/master/terms.md#-4-obligations-of-the-customer).

The **up-to-date mindset** requires some thinking ahead and discipline. [Technical debt](https://en.wikipedia.org/wiki/Technical_debt) is the keyword here. Consider upfront that all the code your are having out there, will constantly need some attention and time.

It's easier when you are code maintainer and business owner, like with a start-up or as a freelancer on your own projects. It's more complicated in bigger structures and in client-agency relationships. Make maintenance an topic early on, include it in your estimates. **Raise awareness on the importance to keep your software up-to-date.** Reserve a time budget for that upfront.

## Our next steps

We will provide further information — in much more detail and hands-on — on how migration to PHP 7.2. And we will also inform clients individually on affected Apps soon. There will be multiple mailings. We currently plan to update all remaining Apps to **PHP 7.1** in February 2019, an exact date will be announced. Feedback and questions are — as usual of course — highly welcome.

## Wrapping up

We are very happy to see the PHP language under heavy development coming closer to shorter release cycles and even breaking some old habits. It's alive. Let's embrace change and move forward.
