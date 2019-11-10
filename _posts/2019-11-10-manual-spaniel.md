---
layout: post
author: Kat
title: Manual Spaniel
tags: [documentation]
---
On an active project, technical documentation can go stale pretty quickly. Stuff gets iterated! Stuff gets upgraded! Throwaway chunks of code become key production features! Key production features get deleted once they are found to be not so key as originally thought!

As a team, we're pretty good at updating our developer manual as and when we make a change to our code or infrastructure. But things still get missed, for example if an outdated tool or component is briefly mentioned in an otherwise unrelated page. To help sweep up these leftovers, our team carries out a 'Manual Spaniel' process every quarter. 

The name 'Manual Spaniel' originally comes from a Slack reminder bot called Daniel the Manual Spaniel - that our team doesn't actually use! Our process is, ironically, more manual: at the beginning of the quarter (usually coinciding with the team firebreak), one person on the team will create a spreadsheet listing all the manual pages and how long ago they were updated. This is usually copied directly from the manual's github repo. That person (ok fine, it's me) then shares the spreadsheet with the rest of the team, using the appropriate number of dog emojis.

Each developer then assigns themselves some pages to review. There's a bar chart showing how many pages each dev has reviewed, to highlight who's doing more or less than their fair share! There's another column to add in any pull requests that get raised, or a 'N/A' if the page doesn't need any changes.

It's a good idea to assign yourself to a page you're unfamiliar with, or that you didn't look at the previous quarter, to share knowledge widely around the team. I don't have much patience with "_but I don't know enough about this topic to review it_" - it's the manual! It should be self-explanatory, right? If someone is relatively new to the team, we try to be kind and assign them the 'getting started' page, and see if it matches up with their experience.

The reviewing itself should not be an in-depth rewrite or reorganisation of the page - none of us are technical writers and we only allow ourselves a week to review 50-odd pages. The Manual Spaniel prorities are: 

- correcting factual inaccuracies (outdated version numbers, misleading typos, a recent change to a process) 
- fixing broken stuff (links, linting errors) 
- removing stuff we don't need
- reviewing pages that haven't been touched in a long time 

It's sometimes really tempting to do a major rejig of a page, or create a brand new page for something missing. If that's really necessary, then it's probably a candidate for a separate story ticket, to be prioritised accordingly. Hopefully, our regular 'spanielling' means these cases are few and far between.

Next quarter I may look at automating some of the process (a Better Setter?) and speeding things up.
