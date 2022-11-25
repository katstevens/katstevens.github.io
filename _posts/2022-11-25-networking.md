---
author: Kat
title: Networking 
layout: post
tags: [networking]
---

Not the meeting people kind of networking - the kind where you send messages over the internet. Although I suppose people meet each other that way too.

For the last few months my team has been unravelling some fairly knotty Terraform, most related to AWS networking - VPCs, subnets, security groups, and of course the odd bit of DNS wrangling. There's so much to learn about this topic: where do you start?

A great primer is [Julia Evans](https://jvns.ca/)' excellent [Networking Zine](https://jvns.ca/networking-zine-coloured.pdf), which explains (in just the right amount of detail) all those awful networking acronyms: HTTP, DNS, TCP, CIDR, SSL. The main reason I've written this blog post is to share this more widely, as it's so useful.

After a few years of working on an infrastructure team, I feel like I've finally got a handle on all of these terms, and can keep them straight in my mind without looking them up. Just in time for everyone to ditch TCP completely and move onto [HTTP3/QUIC](https://www.cloudflare.com/en-gb/learning/performance/what-is-http3/)!
