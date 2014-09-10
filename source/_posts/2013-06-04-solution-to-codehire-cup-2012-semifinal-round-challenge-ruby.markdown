---
layout: post
title: "Solution to Codehire Cup 2012 Semifinal Round Challenge [Ruby]"
date: 2013-06-04 01:09:30 +1000
comments: true
categories: [ Cup ]
author: Dan Draper
---

### A solution in Ruby to the Semifinal Challenge in the inaugural Codehire Cup held in September 2012 at the University of Adelaide.

In September 2012, Codehire held the inaugural Codehire Cup in Adelaide, featuring some relatively simple coding problems. Contestants could choose to use C#, Java, JavaScript, PHP, or Ruby to submit solutions through a web-based interface. Fastest contestant wins.

## The Problem

The Cup Semi-final problem read:

Calculate the result of the expression.

The input string will be random but will only contain the numbers one through nine and the plus and minus operators. No operator precedence rules need be applied.

The input may include up to 10 operators.

Your result should simply be an Integer cast to a string.

Example:

    five plus four plus six minus seven

Result: 8

## The Solution

The problem is made trivial by the built-in Ruby `eval` method: we simply need to replace ‘plus’ with ‘+’, ‘minus’ with ‘-’, and each digit specified as a word with the same digit as a numeral.


nums = 'zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'

{% codeblock lang:ruby %}
str = input.gsub('plus', '+').gsub('minus', '-')
nums.each_with_index do |s, i|
  str.gsub!(s, i.to_s)
end
output << eval(str).to_s
{% endcodeblock %}

## Another Solution

If we didn’t have the built-in Ruby `eval` method, we’d have to be more clever.

{% codeblock lang:ruby %}
nums = 'zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'

res = nums.find_index input[/^[a-z]+/]
input.scan(/plus ([a-z]+)/)  { |m| res += nums.find_index m[0] }
input.scan(/minus ([a-z]+)/) { |m| res -= nums.find_index m[0] }
output << res.to_s
{% endcodeblock %}

We thank <a href="https://plus.google.com/+ChrisDziemborowicz/posts" rel="author">Chris Dziemborowicz</a> for making his solutions to the previous cup challenges public. Chris won last year's event so who better to guide you through the challenges!
