---
layout: post
author: Kat
title: Reading vs Reviewing
tags: [code reviews]
---
Our team produces on average a dozen pull requests a day, sometimes more if one change needs to be replicated across many apps. I try and read all of them. Yes, all of them.

This sounds like madness, but bear with me. 

## tl;dr (took a look; didn't review)

‘Reading’ a PR is not the same as ‘reviewing’ a PR. For me, reviewing a PR means a thorough inspection of the code, checking out the branch and running local functional tests (I, er, definitely always do this, ahem), and thinking carefully about how it will be deployed, any possible side effects etc. There are guidelines on good code reviewing practice on the [GDS way](https://gds-way.cloudapps.digital/manuals/code-review-guidelines.html), so I won’t get into that here.

When I say ‘reading’, I mean reading the description, skimming the changes, and deciding if it warrants a closer look. Github email notifications don’t say whether a PR is a draft or not (it’s a relatively new feature, after all), so if I click through to a draft I’ll close the tab and archive that email until it pops back up again. If it’s a boilerplate change that I’ve already seen in another app, I’ll skip and move on. If I spot something interesting/unusual/problematic I might drop a quick comment or question. If it’s a knotty, complex beast of a PR I will roll up my sleeves and give it a proper review! But I will have to make proper time for that, as a good review shouldn’t be rushed.

## Managing it all

Obviously this is a lot of PRs to keep track of. Some folks on the team use specific tools or plugins to help with this, but usually I just keep track of the Github notification emails in my inbox (which is normally near-zero, because I snooze a lot of stuff!). We also have a dedicated team Slack channel for asking for reviews, and a [Sealbot](https://github.com/binaryberry/seal) that gives us daily reminders of lonely, neglected pull requests in need of attention. I'll prioritise these over bog standard email notifications. 

My ‘click through then archive the email’ method also helps me keep track of discussions and any questions I need to respond to. If I don’t have to do anything right now, I will archive that email until it pops up again and concentrate on something else.

## But why, tho

So, why do I want to read everything? Well, I like having an overview of what’s happening on the site. As previously mentioned, I do more talking than coding, so it’s useful to be able to talk about the coding that other people are doing. I like knowing who raised a PR, so that even if I don’t know the finer details of the change, I know who to ask about it later. I like knowing if two people are doing bits of potentially clashing work, so I can tell them to speak to each other. 

This is a sustainable process for me at the moment because our team only has a handful of developers and around 20 active repositories. Though saying that, if our team was double the size, we’d probably be dividing our efforts more and I’d be watching fewer repositories as a result. If I’ve been away on holiday and the PRs have built up to 100+, my skim-reading certainly becomes more superficial! But going through the backlog is also a quick way to catch up on what’s been happening. 

I absolutely wouldn’t expect everyone to exhaustively read PRs in this way - it’s a method that works for me, with my zero inbox and short attention span, and my all-consuming desire for omniscience. I am reading all these PRs so that you don’t have to!
