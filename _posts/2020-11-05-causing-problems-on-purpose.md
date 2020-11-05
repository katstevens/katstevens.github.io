---
layout: post
title: Causing problems on purpose
author: Kat
tags: [tests, errors, game days, virus checking]
---

Our household is fond of the [Untitled Goose Game](https://goose.game/) and its refreshing moral approach. 
The idea is to complete a number of tasks designed to annoy the townsfolk as much as possible. 

![Image description: meme of the Goose on a picnic blanket, with the legend ‘I think I will cause problems on purpose’](https://i.kym-cdn.com/photos/images/newsfeed/001/629/979/569)

Intentional errors are very useful in software engineering. Let's take a look.

## Unit tests

Tests aren't just about the happy path. Error cases always seem to be the last bit of code to get test coverage, even though it's your first line of defence to make sure your code is robust.
Often the unhappy path is neglected because it feels 'difficult' to set up or assert the error conditions. I promise you it's worth it in the long run, especially when you end up having to investigate [Detective Pikachu errors](https://katstevens.github.io/2019/11/03/detective-pikachu.html) later down the line and need a handy list of all your error scenarios.

The [pytest docs give some simple examples, to get you started](https://docs.pytest.org/en/stable/assert.html#assertions-about-expected-exceptions). 

## Intentional 500s

Let’s say you’ve recently made some changes to your monitoring/alerting tools. You’ve hooked up your apps and checked all the configuration. 
No errors! Congratulations on such a squeaky clean app, job done… or is it just that the errors are never reaching the alerting tool? 

It might sound counterintuitive but it’s useful to have a way of ‘breaking’ your app in a controlled way, at least temporarily. 
Consider having a protected view along the lines of `/trigger-500-error` which you can use to generate an error on your terms, giving you time to warn your support rota and ignore it in the parts of your pipeline you’re not testing.
Document it carefully so everyone knows what it's for and when to use it.

## Fake viruses

Similarly, how do you test your application’s antivirus software is working? 
At GDS we have some projects using [clamav](https://www.clamav.net/) for virus scanning. 
If one of our users uploads a file containing a virus, an alert is triggered.

Obviously we don’t want to upload a real virus to our system to make sure the alerts are working, so instead we use an [EICAR file](https://www.eicar.org/?page_id=3950) - a file with a recognised signature that `clamav` treats as it would a real virus. 
This file can be uploaded as part of a [regularly scheduled smoke test](https://github.com/alphagov/digitalmarketplace-functional-tests/blob/master/features/smoulder-tests/antivirus/antivirus.feature), and we get an ‘ignorable’ notification about it. 
If that smoke test fails, we know there’s likely a problem with `clamav`.

## Static error page views

Hopefully your website has one or more static error pages (aka the 'failwhale'), that users will see alongside 5xx or 4xx status code responses. 
Hopefully you also want to test what it looks like in production, without triggering a bunch of unwanted error alerts.

One option is to add a specific view (such as `/errors/404`) that renders the given error template, but with a 200 status code. 
The [Django docs give a quick example](https://docs.djangoproject.com/en/3.1/topics/http/views/#testing-custom-error-views) of how to set up such a view and write a unit test for it, although that view returns a ‘real’ error status code.

In a production scenario you’d have to take care to make this view difficult to discover by real users (or bots), but still close enough to production conditions that you can test that things like static assets are rendering correctly and/or using appropriate caching.

## Unleash the Chaos Monkey

The real life Untitled Goose! Netflix developed the [Chaos Monkey](https://netflix.github.io/chaosmonkey/) tool in 2011, that randomly disables things in their production infrastructure (shudder) to test their resilience and recovery times. 
The [code is open source](https://github.com/Netflix/chaosmonkey), go have a look! This sounds completely terrifying.

A slightly less scary version is to run game days on your test environment. 
One or two members of the team play the role of an attacker (kiddie hacker, disgruntled employee, Godzilla taking out eu-west-1, etc) and the rest of the team has to sort it out. 
It’s a good test of the team’s incident processes in what should (hopefully!) be a less stressful situation than a real incident. It's also useful for getting to know your infrastructure better - which bits of your app could cope without a database? 
Note that it’s a good idea to disable everyone’s production access during game days, just in case someone’s fingers start typing `prod...` on autopilot.
