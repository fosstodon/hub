---
title: Fosstodon and Cloudflare
author: kev
description: We've been asked a lot of questions about our use of Cloudflare, so here's our official stance.
layout: post
---
{: .notice}
As of 23rd August 2023, Fosstodon is fully migrated to Fastly, which mean we no longer use Cloudflare in any form, not even for DNS.

Today, I went looking through the [#Fosstodon](https://fosstodon.org/tags/Fosstodon) feed, and in there I saw a number of comments about our use of Cloudflare and how that's really bad.

Let me start by saying that using Cloudflare isn't great - [we've talked about this before](https://hub.fosstodon.org/moving-away-from-cloudflare/), but that was when we were much smaller and when we weren't the subject of [the occasional DDoS attack](https://hub.fosstodon.org/elon-twitter-post-mortem/).

Yes, we use Cloudflare. We do so because their DDoS mitigation is effective and the alternatives are prohibitively expensive for us. We do, however, use Cloudflare in a very specific way:

* We don't use their certificates, so they can't content inspect *any* traffic from Fosstodon
* We don't use the Cloudflare CDN, we use [Bunny](https://bunny.net) instead
* Under normal circumstances, we don't even proxy traffic through their service, so Cloudflare is just a DNS provider for us
  * If you want to prove this for yourself, ping `fosstodon.org` - it should resolve to `54.38.247.97` which isn't one of [Cloudflare's IP addresses](https://www.cloudflare.com/en-gb/ips/)

When we're under attack, that changes though. We switch on the proxy and the anti-DDoS mitigations that Cloudflare offer. This is so we can maintain the service we provide to, like, 60,000 people. Once any attacks stop, we turn it all off again.

{: .notice}
When we're under attack and using their proxy, Cloudflare can, unfortunately, content inspect our traffic.

## Fastly

After the wave of DDoS attacks we received a few months ago, Fastly reached out to us and kindly offered a complimentary account on their service so we could have DDoS mitigation and a CDN for free.

This was an incredibly generous offer, which we took them up on. But the problem is, their service is extremely difficult to navigate, so neither myself or Mike have been able to work out how to configure it all.

If any of you out there are familiar with Fastly's service, and are willing to help us configure it, please [get in touch](https://hub.fosstodon.org/contact/) as we would love to get off Cloudflare if possible.

Until we can get Fastly working, Cloudflare will remain a necessary part of the Fosstodon stack, I'm afraid.

