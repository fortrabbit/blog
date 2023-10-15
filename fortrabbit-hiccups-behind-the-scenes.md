---

title: Hiccups
author: fl
excerpt: "Behind the scenes when something goes wrong."
created: 2013-05-21

---

**Not an easy post to write:** During the last two weeks a few of our customers had to experience some downtimes. Read here what basically is going on and what that means to us.

Our "PHP as a Service" just started last October. So far everything had just worked flawlessly and the customer feedback is tremendous. We know that the hosting business is a lot about trust. We have been hosting websites on our old bare metal solution for quite some while, but that is something, not everybody knows. A new service is suspect anyways. When something fails here, it can get quite a drama. 

> Performance, reliability & security are most important in hosting. Equally most important is developer happiness.

We have seen the error occur all of a sudden for the first time about a month ago: One of our nodes had an unusual load-peak. It was killed and restored within a few minutes. This can happen and should not be a big deal. Unfortunately the load problem reappeared on a completely different node some days afterwards. We stopped the line (all development of new features) and concentrated our energy on fixing this. Soon it became clear that it was a networking problem, resulting in a high load on the node. In the start, the event was so seldom, it was hard to catch it and run tests while it occurred. Towards the end of last week, with no good reason, the frequency of the events increased (~two nodes a day). Now the interval seems to move back again to as it was before. Since we started investigating we have ran** thousands of tests** to nail the source of the issue down. So far, we can exclude a lot of possible reason but have not finally found the actual source of the problem - but we're zooming in. I am very happy with the sympathetic feedback of our customers – didn't expected that. **Thank you so much for your understanding.** I really really hope that i don't have to write another post of something that failed very soon. We do the best we can here. I guess most of you guys haven't noticed the issue, since it happened only to a few nodes so far and it usually took only 10 minutes until the system automatically recovered. Apps running on a high availability plan have also not been affected. For us this issue is really a pain, but we're confident to finally resolve it this week or the next. We will keep you updated. 

* * *

**UPDATE 1** 2013-05-22: If you are have deep SysOp knowledge or you are just curious: **[TCP Dup ACK**](https://www.google.com/search?q=TCP+Dup+ACK) might be the trigger of the issue. 

* * *

**UPDATE 2** 2013-05-24: We finally got to the root of the issue and were able to resolve the main problem. We're still monitoring our systems carefully for recurrences but are confident it's gone for good.