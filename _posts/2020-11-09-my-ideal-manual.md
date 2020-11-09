---
author: Kat
title: My ideal manual
layout: post
tags: [documentation]
---

I’ve been thinking about developer docs for the past few weeks, and how they can be improved. To do that, we have to know ‘what good looks like’. Here’s my short definition of a good developer manual:

1. Everyone on the team (developers and non-developers) uses it regularly
2. Everyone on the team (developers and non-developers) can keep it up to date
3. Everyone can find what they’re looking for quickly.

Let’s dig in a little deeper into each of these.

## 1. The whole team uses it

This might seem obvious, but there’s no point having a developer manual that no-one uses. Broken down a little further, this should also mean that:

- It’s accessible enough for inexperienced team members to use as a learning resource
- It’s detailed enough that experienced team members still use it as a reference guide
- It’s accurate enough that all team members are confident that the information in the manual is correct

The team manual is pretty much permanent fixture in my browser tabs.  I’m relatively new to my current team so there’s a huge amount of detail I haven’t even touched yet. But even after three years on the Digital Marketplace team, I was still looking things up in the manual every day - or telling other people to look things up there. 

Ideally a developer manual should be public: the path of least resistance. If that’s not an option for your team, at least make it easy to access for the set of users who are allowed to use it, e.g. with IP restriction or single-sign-on, rather than a username and password.

But no-one will bother looking at the manual at all if the information itself is out-of-date, hard to find, confusing, or just plain wrong. You will know if this is the case, because the team will keep asking the same questions on Slack over and over again.

## 2. Everyone can update it

Pages are more likely to be accurate if:

- it’s easy to make changes
- people aren’t afraid to delete old/wrong stuff
- documentation is part of the regular workflow 

Having version control on a manual (say, in Github) is obviously useful in terms of keeping a history of changes, submitting pull requests for a 2nd opinion and so on. It also removes the fear of deleting stuff - you can always get it back if you need to!

Of course this does create an extra layer of complexity for making small updates (eg fixing broken links/typos, updating ‘last updated’ dates), especially if the person isn’t used to the git workflow. Personally I prefer it - manual updates can be a great low-stakes introduction to writing your first pull request!  But a good documentation process will take into account the needs of its users. If having a wiki-style manual (say, in Confluence) makes more sense for your team, by all means go for it.

Last year I wrote about the [Manual Spaniel](https://katstevens.github.io/2019/11/10/manual-spaniel.html) which worked pretty well as a quarterly blitz to keep the Digital Marketplace manual up to date. Some GDS teams also use a Slack bot prompt, that checks the ‘last updated’ date on each manual page and pesters people to review overdue pages, though this requires people to remember to update that date when they do review it! 

Manual Spaniels are all well and good but ideally documentation should be part of the team’s workflow. Plan for it as part of your feature. Write things down as you go!

## 3. Quickly finding what you need

Different team members will have different needs here.
 
- Old hands wanting to find a command line shortcut might want a decent search box, that mostly works like Google. 
- New starters might want a well-structured index for browsing, and some detailed step-by-step guides for onboarding and team processes. 
- Technical architects might head straight to the diagrams and Architectural Decision Records. 
- Product managers might want a high level summary of a feature, to share with stakeholders. 
- Nosy devs from other teams might want to sneak a quick peak at what tooling and infrastructure you’re using, so they can compare notes.

There are lots of ‘might’s there. If you’re not sure, ask the team and find out what they want from their manual.

Once you’ve got that info, you’re ready to start shaping your manual into a useful tool. But that’s for another blog post…
