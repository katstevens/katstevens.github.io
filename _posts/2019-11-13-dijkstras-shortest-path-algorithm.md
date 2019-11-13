---
layout: post
title: Dijkstra's Shortest Path algorithm
author: Kat
tags: [actual computer science, algorithms]
---
## I tied an onion to my belt, it was the style at the time

At university I was taught all manner of things that were completely irrelevant to my current job of building and maintaining modern web applications. Perhaps one day I will need to [interpolate a cubic spline](https://en.wikipedia.org/wiki/Spline_(mathematics)), but so far I have managed without them. [Pierre Bézier](https://en.wikipedia.org/wiki/Pierre_B%C3%A9zier) can rest easy.

I think I sensed at the time that splines and their like weren't really for me. Some stuff on the syllabus was both interesting and useful, however! [Dijkstra's Shortest Path algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) was a favourite of mine, because: 

- a) I could immediately see a practical use for it 
- b) I could actually understand what the hell was going on, even when hungover
- c) It had a memorable name that I have heard pronounced different several ways since.

I decided to base my final year project on it. This was the only module I got a decent mark on: see point b).

## What does the algorithm do?

The problem is simple: find the quickest way of getting from A to B. 

Let's say you are at Charing Cross tube station. What's the quickest way of getting to Covent Garden station? A quick tap on the TfL website will tell you to take the Bakerloo line to Piccadilly Circus, then change for the Piccadilly line two stops to Covent Garden. A Londoner will tell you to bloody well walk, it's not that far, and would actually involve less walking than taking the tube.

All those possible stations and tube lines can be represented by a big web of interconnected dots (or 'nodes') and lines (or 'edges').  Each line will have a 'weighting', usually representing distance, minutes or effort (if say, you want to avoid walking). 

In our example, we have 3 nodes:
- A: Charing Cross
- B: Piccadilly Circus
- C: Covent Garden

There are three edges, with different weightings:

- A-B: Bakerloo line (1 min)
- B-C: Piccadilly line (2 min)
- A-C: Walk (10 min)

It seems reasonable for TfL to suggest we travel via A-B and B-C, as 3min < 10min. The Londoner would state that these weightings do not take into account being stuck behind tourists with huge suitcases when trying to get on the lift.

This is a very small map with only two real choices. Think about how many choices there would be if we added in extra edges for buses, cycle hire or taxi. Think about how many choices there would be if we were travelling from London Bridge to Paddington! 

You could traverse all the possible routes between A and B, and keep track of the 'cheapest' route, but spoiler: this would take blimmin' ages.

## What makes Dijkstra's algorithm good?

The algorithm itself is really efficient, in computational terms. Instead of comparing every possible route or expending effort trying to determine the 'right' direction to go in, it methodically builds up a network of the cheapest routes by 'visiting' all the nodes a maximum of once, and keeping track of the best route as it goes. 

A 'visit' isn't trivial though - it involves checking a node's unvisited neighbouring nodes to see if any of them can offer a shorter route. The other good news is that number of unvisited nodes will keep getting smaller, so each subsequent 'visit' takes less and less time. 

We also have to maintain a suitable data structure to keep track of which nodes we have and haven't 'visited', and their current weightings. Luckily for us, if we use a fancy data structure like a [Fibonacci heap](https://en.wikipedia.org/wiki/Fibonacci_heap) (or something appropriate to your data set), then it will be even more efficient! 

The [wikipedia page](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) goes into more detail about what a 'visit' entails, and has a nice animated diagram. Go have a look!
