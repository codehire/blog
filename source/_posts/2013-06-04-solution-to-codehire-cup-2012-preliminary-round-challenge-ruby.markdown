---
layout: post
title: "Solution to Codehire Cup 2012 Preliminary Round Challenge [Ruby]"
date: 2013-06-04 01:01:33 +1000
comments: true
categories: [ Cup ]
author: Dan Draper
---

### A solution in Ruby to the Preliminary Challenge in the inaugural Codehire Cup held in September 2012 at the University of Adelaide.

In September 2012, Codehire held the inaugural Codehire Cup in Adelaide, featuring some relatively simple coding problems. Contestants could choose to use C#, Java, JavaScript, PHP, or Ruby to submit solutions through a web-based interface. Fastest contestant wins.

## The Problem

The Codehire Cup Preliminary problem read:

A train travels from point A to point B, C, D and so on. The travel between two points is a straight line and can be described as a vector (heading and distance). Heading can be any of N, S, E, W, NE, SE, SW or NW (referring to points on the compass) and distance is an integer in km.

The train’s travel can be read from input in the following format:

    (<start point>:<end point>)[<heading>:<distance>],(<start point>:<end point>)[<heading>:<distance>],…

For example:

    (A:B)[N:100],(B:C)[NW:50],(C:D)[E:75]

Your program should calculate the distance the train has traveled as the crow flies (i.e.; a straight line) between the first point encountered and the last (in this case between points A and D).

Simply write your result in km as a rounded integer converted to a string.

Eg:

{% codeblock lang:ruby %}
Output.write("100")
{% endcodeblock %}

## The Solution

This is a simple vector addition problem, so the order that you add the individual hops and the names and locations of the stops are unimportant.

{% codeblock lang:ruby %}
angles = { "SW" => -135, "W" => -90, "NW" => -45, "N" => 0,
  "NE" => 45, "E" => 90, "SE" => 135, "S" => 180 }

x, y = 0, 0
input.scan /\[(.*?):(.*?)\]/ do |heading, dist|
  angle = angles[heading] * Math::PI / 180
  x += dist.to_i * Math.cos(angle)
  y += dist.to_i * Math.sin(angle)
end
output << Math.hypot(x, y).round.to_s 
{% endcodeblock %}

Because we treat the problem as a vector addition problem, we assume that the input string specifies a valid route.

For example, the solution does not check if the train travels from A to B, and then from C to D. The algorithm should return an error given such an input ordinarily, but under contest conditions there is not time for such checks unless they are explicitly required.

We thank <a href="https://plus.google.com/+ChrisDziemborowicz/posts" rel="author">Chris Dziemborowicz</a> for making his solutions to the previous cup challenges public. Chris won last year's event so who better to guide you through the challenges!
