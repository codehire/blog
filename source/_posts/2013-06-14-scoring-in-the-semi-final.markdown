---
layout: post
title: "Scoring in the Semi-final"
date: 2013-06-14 12:38:20 +1000
comments: true
categories: [ Cup ]
author: Dan Draper
---

Scoring of results in the semi-final challenge will be based on three components:

* Your time-to-solve (shorter times are better and if you run out of time you forfeit the round)
* Qualitative assessment of your approach to solving the problem
* Qualitative assessment of your use of syntax, formating and style for your chosen language

## Score Components

### Time

T will be the total available time (for the semi this will be 60 minutes or 3600 seconds) with t representing your time-to-solve.

    s1 = (T-t)/T

### Approach

    s2 = (0..10)  # Score out of 10

### Style

    s3 = (0..10) # Score out of 10

## Final Score

Your final score will be combined as follows:

    S = 250 * (2 * ((T-t)/T) + s2/10 + s3/10)

Giving you a final score out of 1000.

Note that its actually not possible to get a score of 1000 as this would require a time-to-solve of 0!
