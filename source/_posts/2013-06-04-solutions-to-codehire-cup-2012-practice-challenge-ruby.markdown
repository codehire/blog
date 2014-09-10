---
layout: post
title: "Solutions to Codehire Cup 2012 Practice Challenge [Ruby]"
date: 2013-06-04 18:23:30 +1000
comments: true
categories: [Cup]
author: Dan Draper
---

## A solution in Ruby to the Practice Challenge in the inaugural Codehire Cup held in September 2012 at the University of Adelaide.

In September 2012, [Codehire](http://www.codehire.com) held the inaugural Codehire Cup in Adelaide, featuring some relatively simple coding problems. Contestants could choose to use C#, Java, JavaScript, PHP, or Ruby to submit solutions through a web-based interface. Fastest contestant wins.

### The Problem

The Practice Challenge read:

Given an input string (of no more than 300 characters in length), parse the string and count the occurrences of vowels and consonants. The data should be output in the format below (ie; JSON). Punctuation, numbers and any other characters should be ignored.

    {vowels:,consonants:}

    eg:

    {vowels:10,consonants:9}

### The Solution

The simplest solution is to use the built-in Ruby `count` method to count the vowels and consonants:

{% codeblock lang:ruby %}
str = input.downcase
num_vowels = str.count "aeiou"
num_consonants = str.count "bcdfghjklmnpqrstvwxyz"

output << "{vowels:#{num_vowels},consonants:#{num_consonants}}"
{% endcodeblock %}

### Another Solution

It became somewhat of a contest to see who could squeeze a solution to this problem into the fewest number of characters. Bearing in mind that the input string may contain characters that are neither vowels nor consonants (such as whitespace or punctuation), my solution in 93 characters is set out below:

{% codeblock lang:ruby %}
output<<"{vowels:#{v=input.scan(/[aeiou]/i).size},consonants:#{input.scan(/[a-z]/i).size-v}}" 
{% endcodeblock %}

We thank <a href="https://plus.google.com/+ChrisDziemborowicz/posts" rel="author">Chris Dziemborowicz</a> for making his solutions to the previous cup challenges public. Chris won last year's event so who better to guide you through the challenges!
