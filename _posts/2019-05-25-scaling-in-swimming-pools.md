---
layout: post
author: Kat
title: Scaling in swimming pools
---
This week, [our platform was dealing with about 17 times the amount of traffic it normally gets](https://twitter.com/GOVUKdigimkt/status/1131228311684829184). We scaled up the number of apps powering the platform, and aside from the odd bumpy patch here and there, the site hung on and did its job. 

I was telling my parents about this over dinner, and Mum asked what 'scaling' meant. She's smart, but not technical, so this is the analogy I used (yes, of course it is a swimming related analogy):

You're managing a swimming pool [a website], which needs water [memory] to keep the swimmers happy. While most of the water stays in the pool, the swimmers are splashing about and the water needs topping up every so often. You ask a handsome lifeguard [your app instance] with a bucket to top up the water every so often, and this is usually enough. 

Now it's a really hot day - the pool is heaving. You employ extra people [more app instances] to carry buckets and top up the water. Soon they're carrying two buckets each [more processes per app], and for some reason there is still not enough water in the pool. Our team spent a reasonable amount of time this week wondering whether there was a hole at the bottom of the pool [a memory leak], or whether some of our lifeguards had skived off work without telling us [app instance crashes], or whether there were holes in the buckets [dear Liza]. It was probably a combination of factors, but we think we've got a better idea of where to look for holes now. Eventually we gave each lifeguard bigger buckets [doubled the memory allocation per app instance] and this seemed to finally keep the water level stable. 

Now the deadline's over, the sunny spell has ended and most of the swimmers have gone home. We can give our extra lifeguards their P45s [scale back down to normal instance numbers/memory allocation]. And we're all off for a long weekend!
