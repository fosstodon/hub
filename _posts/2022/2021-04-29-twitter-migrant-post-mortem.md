---
title: Twitter, Elon & Fosstodon - A Post-Mortem
author: kev
description: We were effectively DDoS'd by Twitter migrants following Elon's purchase of Twitter. Here's what we were doing in the background.
permalink: /elon-twitter-post-mortem/
layout: post
---
If you haven't heard, Elon Musk [recently agreed a deal to buy Twitter](https://www.telegraph.co.uk/technology/2022/04/25/elon-musk-buys-twitter-deal-price-takeover-share-price/) for a whopping $44bn. That cause a little turmoil over in Twitter land, which resulted in expats coming over to Mastodon in their droves.

Because we're one of the biggest technology focussed instances on the Fediverse, **a lot** of people requested an account on Fosstodon. As you can see from the graphs below, the spike in users from Twitter made our usual activity almost flat line:

![Fosstodon user stats with spike](/assets/images/fosstodon-user-stats.webp)

This effectively resulted in a sustained DDoS that lasted for around 36 hours. As you can imagine, that was a lot of fun for myself and the team.

Here's the details of what happened during those 36 hours...

## Sidekiq limits
Before I get into the detail of what happened, it's important to give you some context as to how communication between instances works on Mastodon from a technical perspective. The whole thing is more complicated that I mention below, but it will give you the gist of what I'm waffling on about when we get into the detail.

Sidekiq is critical to keeping a Mastodon server running smoothly; it's what allows a Mastodon instance to scale and is where we struggled during Musk-gate. Sidekiq has threads that allow for multiple jobs to be run concurrently. These jobs deal with the communication between instances on the Fediverse.

For example, let's say that I have 1,000 followers spread over 20 instances. If I post something, Fosstodon will need to let those 20 instances know that I have created a new post, so they can fetch it and show it to whichever users on that instance follow me. 

This sounds like a lot of work, right? But an instance with a couple of threads could easily do this in a few seconds, but scale that up to over 20,000 users and it's **a lot** of activity. So before the influx, Fosstodon had 25 Sidekiq threads to deal with the load.

If the threads become overwhelmed then Sidekiq maintains a queue that Mastodon will chug through as and when it can. 

Under normal load, our 25 Sidekiq threads would max out at around 300 jobs in the queue, which would easily be cleared well within a minute. Can you see where this is going, folks?

{: .notice}
If you want to learn more about scaling a Mastodon server, take a look at [the official docs](https://docs.joinmastodon.org/admin/scaling/).

## Something is wrong here
It all started on Monday evening as the news of Musk's takeover of Twitter broke. It was my good pal and co-admin, [Mike](https://fosstodon.org/@mike) who first noticed that things were feeling at little sluggish on Fosstodon.

We then started to notice a *significant* uptick in new account requests. To give you an idea, we get around 20 new account requests on an average day. Once the news broke, we started to see approximately 1 new account request **every minute**.

By way of a side note; every account request is manually reviewed and approved/denied. This is to stop spammers and bots from getting on our server. So you can imaging that this a **a lot** of work for [our small team](/team).

Anyway, Mike took himself off and had a look at the Sidekiq queue and could see there was a couple  thousand jobs in the backlog.

**Uh oh**.

The team jumped into action and we carved up the workload:
* Coop, Tay0 and Ru were trying to get through the backlog of new user requests as quick as they could.
* Mike and I were keeping a **very** close eye on the server status and working with our host, [Masto.host](https://masto.host) to see what we could do about the traffic.
* Mike and I were also jumping in and helping with the account requests whenever we had time to.

## The first upgrade
We decided to monitor the situation for an hour to see how things go. That first hour flew by and the Sidekiq queue grew from 2,000 to 6,000.

We already had Hugo from Masto.host lined up and we agreed to increase our Sidekiq threads from 25 to 30 to try and at least stop the backlog from growing further. At this point, lots of users were also starting to notice the sluggish performance and things like a lack of notifications due to them being tied up in the backlog.

Hugo and I, who are both in Europe, went off to bed and Mike carried on monitoring the situation. I woke up around 05:30 the next morning and checked our Mattermost channel. Here's what I saw in Sidekiq:

{: .center}
![Fosstodon Sidekiq backlog](/assets/images/fosstodon-backlog.webp)

We're still on 30 threads, all of which are busy and we now have a whopping backlog of **157,523 which was rising!**

## Upgrade number 2
At this point, we got back in touch with Hugo from Masto.host who explained that there was no more juice left in that server. So if we wanted more threads, we needed to migrate to an entirely new server, which would come with around 2-3 hours of downtime.

The team and I took this away and discussed it, but to be honest, there was no discussion to be had. We needed to do this upgrade to keep Fosstodon running. So we agreed and Hugo got to work.

Now, I must say here, I've worked with a lot of hosting providers in my time, but Hugo and Masto.host is by far **the best** service provider I've ever used. Hugo is always really quick to respond to queries, and is super helpful.

If you're thinking about starting your own Mastodon instance, I'd **seriously** consider [Masto.Host](https://masto.host) if I were you.

Around an hour and a half later we were up and running on the new server with **80 Sidekiq threads**. By this time, the backlog looked something like this:

{: .center}
![Fosstodon Sidekiq backlog after upgrade](/assets/images/fosstodon-backlog-upgrade.webp)

All 80 threads are going crazy and we're now at **181,080 in the queue!** Thankfully, the 80 threads were enough for us to get on top of the backlog and a couple hours later things were back to normal:

{: .center}
![Fosstodon Sidekiq backlog complete](/assets/images/fosstodon-backlog-upgrade-complete.webp)

And there it has remained ever since with normal service resuming, albeit still continuing with a large uptick in traffic.

## The fallout
Woooooo, that was a tough 36 hours. I've worked in Cyber Incident Response for a number of years, and this felt somewhat like responding to an incident.

We managed to prevent Fosstodon from falling over, but to do that, we have had to triple the capacity of the server and our hosting fees have risen from $90/month to $220/month. This means that our [usual 6 month float of funding](/longevity-and-fosstodon/) has reduced to around 3 months.

Thankfully, a number of members of the community have stepped up and [supported us](/support), which has helped. Coop, Mike and myself have also doubled the contribution we make each month.

Now we could downgrade again, but we would only be back to square one if we see another significant uptick. So it doesn't seem worth it to us.

The upshot of all this is that our fantastic community has grown even more and the local timeline is bustling with even more activity than usual.

So on behalf of the rest of the Fosstodon team, I'd like to welcome all of the new users to the instance, and simultaneously apologise for the rough ride all our members had for that 36 hours or so.

If you want to throw a few $ in the tip jar, you can [find all the ways to support us here](/support).


