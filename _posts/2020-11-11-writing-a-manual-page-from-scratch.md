---
author: Kat
title: Writing a manual page from scratch
layout: post
tags: [documentation]
---

Good developers don’t have to be good writers. While writing docs, READMEs (and blogs!) comes fairly easily to me, I know a lot of devs struggle with it, especially when there’s a blank page just sitting there, waiting for some text. 

I think it’s a really useful skill to be able to quickly knock out a few paragraphs describing your shiny new thing while it’s fresh in your mind. Like any skill, you can improve it by practicing!

## Where to start?

Let’s say we’re trying to write a brand new manual page for our service’s new Cat Pictures component.

Your best bet is to copy the structure from an existing page for something similar.
Delete all the specific detail straight away (so you don’t accidentally leave in unrelated info) but keep generic headings like ‘Getting Started’, ‘Troubleshooting’ and so on.

Next, jot down the important bits, fresh from your brain, as bullet points. 

- replaces old Dog Pictures component
- need info on how to integrate with Pet Gallery, that's not obvious
- reminder that cat number 14 is actually a tiger, yikes
- VPN access required for secret cats

Now add some what/where/how questions to the list:
- what is it?
- where is it?
- how do we use it?
- who should use it?
- why are we using it?
- when did we start using it?

The last three (who/why/when) may not apply to your page, but if you have that info to hand, stick it in.

Let’s group these bullet points, questions and rough answers (if you have them) into the section headings. 

```
## Introduction
- What is it? (Cat picture resource for devs)
- Where is it? (link - http://example.com/catpictures)
- Replaced old Kitten Pictures component in Nov 2020

## Getting Started 
- How do we use it?
- info on how to integrate with Pet Gallery
- VPN access required for secret cats

## Troubleshooting
- reminder that cat number 14 is actually a tiger, yikes
```

Now you can flesh it out into something human-readable:

```
## Introduction
[Cat Pictures](http://example.com/catpictures) is an app that generates semi-random pictures of cats in PNG format, for use by devs in their blog posts.

It replaced the old Kitten Pictures component in Nov 2020.

## Getting Started 
Clone the repo and install dependencies with `make whiskas`. 

Set the path to Pet Gallery via the environment variable PET_GALLERY=“https://…”

Secret cats require VPN access.

## Troubleshooting
Proceed with caution when using cat number 14, which is actually a tiger, yikes.
```

'Human-readable' is often where people struggle. The good news is that we are developers, not Nobel Prize for Literature contenders. 
As long as your sentence is clear and unambiguous for someone whose first language might not be the same as yours, that'll do. That means no sarcasm! I'm so sorry. 

## Done is better than perfect

Incomplete is also better than non-existent! Don’t be afraid to type ‘TBC’ and come back to a section at a later date, or ask someone else to help you fill in a gap.

Avoid saying things like “we will be changing X to Y next week/year/in the near future” - that’s just asking for project Y to get canned as soon as you commit that sentence. Instead, make it clear what’s happening now, and when ‘now’ is: “As of November 2020, the team is using Kitten Pictures in production and using Cat Pictures for test environments.”.

## Different types of manual page

The example above was for a page describing a technical component. Other types of pages will need a slightly different structure and level of detail.

A ‘how-to’ page should be a sequential set of steps, easily understandable for a new starter with everything spelled out exactly, and plenty of context/detail. 
What will they need to do before they start? When will they need help from a colleague?

An incident process page should be more streamlined, so the important info can be found quickly and unambiguously by stressed-out (but hopefully more experienced) developers.

Keep in mind the audience you're writing for, and you'll be fine!
