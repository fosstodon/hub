---
title: Our Domain Expired and it Took Out All Our Services
author: kev
description: A couple of days ago fosstodon.org expired and all our services went down. Here's how it happened.
permalink: /our-domain-expired/
layout: post
---

It's Saturday evening. It's been a busy day, what with the kids being off school and all. My wife and I are preparing dinner for the family and honestly, I can't be bothered; all I want to do is sit on the sofa and relax.

Something compelled me to check my phone, where I saw an email from our community manager, [Cooper](https://fosstodon.org/@cooper) that said...

> Hey bud,
> 
> I think we might have an issue with our domain provider. Nothing is resolving/connecting on the naked domain or any of the subs (Mattermost, Hub, etc).                    
>  
> Best Regards, 
> 
> Matt Cooper

So I made my excuses to my wife, booted up my laptop and checked myself. Yep, it was all down.

**Bollocks!**

My first thought was maybe it was a hosting problem, but Cooper has already said our [Patreon](https://patreon.com/fosstodon) Mattermost server was down, as well as this very Hub that you're reading now. So it couldn't have been a hosting issue, as they're all hosted in different places.

*It must be DNS*, I thought. So I fired up my terminal to check...

```
% host -a fosstodon.org
  Trying "fosstodon.org"
  Trying "fosstodon.org"
  Host fosstodon.org not found: 3(NXDOMAIN)
```

**Double bollocks!**

*Where the hell has our DNS gone?* Our domain and DNS are provided by NameCheap, so I logged into our account only to find that `fosstodon.org` was listed as `EXPIRED`.

**TRIPLE BOLLOCKS!**

## Grace period
Luckily for me, the domain had *just* expired and we were still within our grace period, so we hadn't lost the domain. Can you imagine what would have happened if someone else had nabbed it!

I re-registered the domain as quickly as I possibly could, and 15 minutes or so later, our services started coming back up. *Fantastic!* Crisis averted.

### But how did this happen?
Well, it's very simple, dear reader. **I'm an idiot.** I had my personal card assigned to the account, and it expired a few months back. Needless to say I didn't update the card details, so the domain couldn't renew.

I don't *think* I received any alerts about it. But saying that, I own lots of domains and get emails about renewals all the time, so it's likely I just dismissed the email.

## Fixing the problem
Instead of updating my card and risking being back in this situation when my current card expires, I flipped the payment service to PayPal, which is where all our funds are stored anyway. So hopefully, this won't happen again.

Apologies for the completely preventable outage, folks. Yes, I'm an idiot. Yes, this was avoidable. Yes, I shouldn't be trusted with this kind of thing.

{: .notice}
If you want to help keep the lights on at Fosstodon HQ, you can [support the project here](/support).