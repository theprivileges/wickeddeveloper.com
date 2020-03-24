---
title: Solving the staircase problem in JavaScript
description: Using String.prototype.padStart to solve the staircase problem in JavaScript
date: 2020-03-23 18:25
header:
    overlay_image: assets/images/challenge/header.jpeg
    caption: "Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/hacker?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
    show_overlay_excerpt: false
category:
    - development
tags:
    - javascript
    - challenge
    - code challenge
    - hackerrank
---

The following is my solution to the [Staircase](https://www.hackerrank.com/challenges/staircase/problem) problem. I'm using [`String.prototype.padStart`](https://devdocs.io/javascript/global_objects/string/padstart) to add the appropriate number of spaces in order to build the rises and making sure to right-align the steps. I also use [`String.repeat()`](https://devdocs.io/javascript/global_objects/string/repeat) to build the steps that make up the staircase.

## Problem

Write a program that prints a staircase of size `n`. Where `n` is an integer. 

### Constraints

- 0 &lt; `n` &le; 100

### Output Format

Print a staircase of size `n` using `#` symbols and spaces.

**NOTE** The last line must have `0` spaces in it. 

## Solution

```js
function staircase (n) {
  for (let i = 1; i <= n; i++) {
    const step = '#'.repeat(i); // create a step
    const rise = String.prototype.padStart.call(step, n, ' '); // Add necessary spaces
    console.log(rise);
  }
}
```

## Demo

[JS Bin](https://jsbin.com/zetoxaj/edit?js,console)