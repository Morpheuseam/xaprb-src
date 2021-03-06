---
title: Review of Scalable Internet Architectures by Theo Schlossnagle
date: "2009-02-21"
url: /blog/2009/02/21/review-of-scalable-internet-architectures-by-theo-schlossnagle/
categories:
  - Databases
  - Reviews
---
[Scalable Internet Architectures]({{< amz 067232699X >}}) by Theo Schlossnagle, InformIT, 2006. 225 pages. Here's a [link to the publisher's site](https://www.informit.com/store/scalable-internet-architectures-9780672326998).

[![Scalable Internet Architectures](/media/book-covers/scalable-internet-architectures.jpg# 3dbook)]({{< amz 067232699X >}})

<!--more-->

It's a great book. Anyone building large systems should read it. Heck, anyone building any system that needs to run on more than one server should read it.

The book got mixed reviews on Amazon, but I really think that's about writing style, not substance. Sometimes Theo takes the reader on a scenic tour of something that doesn't seem to have much to do with the subject matter, and then wraps up by showing how it is actually directly relevant. For example, he spends quite a bit of time talking about why HTTPS inherently poses different scaling problems than HTTP. If you aren't a patient reader, you might bail out before getting to the punch line.

It's a pretty compact book, at 225 pages (plus an appendix on [Spread](http://www.spread.org/)). Theo's writing is terse, even blunt at times. He knows what he's talking about and he expects you to do your part to keep up with him. You need to start at the beginning and read the whole book. This isn't a reference that you can just pick up to get five-minute answers.

The topics are as follows:

*   Scaling Up (and Down)
*   Principles for Avoiding Failure
*   Mission-Critical Environments
*   High Availability. *HA! No Downtime?!*
*   Load Balancing *and the Utter Confusion Surrounding It*
*   Static Content Serving *for Speed and Glory*
*   Static Meets Dynamic *Adding Caches to Reduce Costs*
*   Distributed Databases Are Easy *Just Read the Fine Print*
*   Juggling Logs *and Other Circus Tricks*
*   The Right Tool for the Job

These subjects may not seem to add up to a holistic worldview of scalability, but trust me, it works out that way. Theo uses specific scenarios---in complete detail---to illustrate larger concepts. You have to work to follow him, but the payoff is big. Here's a sample of the conclusion to one excursion into the woods:

> Where are we going with this? ... Each request we passed through the server during our contrived test required 743ms of attention. Of that time, 87ms was *not* horizontally scalable... we were simply attempting to show that some portion of the interaction was dependent on shared, nonscalable resources. We succeeded; now how do we fix it?

Have you ever wondered how to build an architecture that automatically results in website visitors accessing the data center nearest them *in network distance*? No, the answer isn't looking up IP addresses to determine geographic location. There's actually an elegant solution to this problem, and I didn't know it.

What about this one: what's a scalable way to invalidate a cache that lives on the filesystem of many machines at once? What if one of the machines doesn't obey is offline or misses the message for some reason?

This book is about how to think scalably. Just as an SQL programmer must learn to think relationally, a person who hopes to design a scalable application architecture must learn to think the right way. And Theo teaches this paradigm better than I've seen it done before.


