---
# This is the page title
title: Moving Away From Cloudflare
# This is the title that shows in the header (usually the same as page title)
header: Moving Away From Cloudflare
# This is the description that shows in the page header
description: A lot of people in open source don't like Cloudflare, so we stopped using it.
# Set a permalink here
permalink: /moving-away-from-cloudflare/
# Don't change this
layout: post
---

We were recently asked by a member of our community why we were using Cloudflare as the [Content Delivery Network](https://en.wikipedia.org/wiki/Content_delivery_network) for Fosstodon.

This was a valid concern considering the [numerous privacy concerns](https://git.nixnet.xyz/you/stop_cloudflare) that many people have when it comes to Cloudflare, especially when it comes to their free TLS certificates and what is basically MiTM TLS inspection. <!--more-->

Now, we want to be *very* clear here **we do not use Cloudflare for our TLS certificate**. That is provided by Let's Encrypt. The only data that is handled by the Cloudflare CDN are the media attachments that our users post.

However, when our members raise a concern, we listen and we try to come up with a solution. We host Fosstodon with [Masto.Host](https://masto.host), which uses the Cloudflare CDN for media by default. Being the great service provider that they are, they give their customers the option to use a different CDN. So we started looking into alternatives...

## BunnyCDN

Kev already uses BunnyCDN for the CDN on his personal website - they're a known quantity and have a good reputation. So we decided to migrate from Cloudflare to BunnyCDN.

Now, BunnyCDN isn't a free service and it may get quite expensive for us to host with them, but we will have to wait and see. We're estimating that the additional cost for BunnyCDN will be around $20/month based on our current bandwidth usage.

Fosstodon is a popular instance, and we generate a lot of traffic. As we grow, that traffic will grow too. At the moment we're funded pretty well and have enough in the donation pot to absorb this additional cost, but if you want to help chip in to keep Fosstodon alive you can [help support us](/support) in a number of ways.

## Conclusion

We will always take the feedback we receive from our community seriously, and we really hope this post proves that.

BunnyCDN is live and serving your content right now. Hopefully the transition has been a seamless one for you. If you do notice a slight slowdown over the next few days, please bear with us as it will take some time for the cache to build up across the new CDN.

![Bunny CDN](/assets/images/bunny-cdn.jpeg)

We will, of course, keep you guys update about how we're finding BunnyCDN. Also, the details of all our funding and how we use can be found on [our about page](/about).

**If you have any feedback, please reach out to one of the team, or [contact us](/contact).**
