---
title: Build a simple calculator
description: A solution to a coding challenge where you are asked to build a simple calculator function that takes a mathematical expression and returns the result of the expression. 
date: 2020-04-13 18:08 +0700
header:
    overlay_image: assets/images/challenge/header.jpeg
    caption: "Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/hacker?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
    show_overlay_excerpt: false
category:
    - development
tags:
  - challenge
  - javascript
  - code challenge
---

The following is my solution to a coding challenge I've come across.  I've implemented it in JavaScript since that is the language I am most comfortable with at the moment.

## Problem

You are building an educational website and want to create a simple calculator for students to use. The calculator will only allow addition and subtraction of non-negative integers.

Given an expression string using the "+", "-" operators like "5+16-2", write a function to parse the string and evaluate the result.

## Constraints 

- Only allow addition and subtraction of non-negative integers.


## Solution

```js
const calculate = (expression) => {
  const numbers = expression.split(/[+,-]/).map(n => Number(n)); // transform String into Number
  const operators = expression.split(/\d/).filter(op => op !== '');
  let result = 0;

  // perform calculation
  numbers.forEach((number, id) => {
    const operator = id === 0 ? '' : operators[id - 1]; // no operator to apply to first number
    switch (operator) {
      case '+':
        result = result + number;
        break;
      case '-':
        result = result - number;
        break;
      default:
        result = number;
    }
  });

  return result;
};
```

[Try it](https://jsbin.com/qacanoy/edit?js,console)

### Explanation

Given the constraints we are working with, I can build my `calculate` function without having to check for negative numbers, and mathematical expressions that do not involve integers.

My first task is to figure out what numbers we are operating on, so I use [`String.split`](https://devdocs.io/javascript/global_objects/string/split) to separate the full expression into substrings of just the numbers by passing the regular expression (`/[+,-]/`) as the `separator` parameter. Since `split()` returns an `Array` of strings, I can call the [`Array.map`](https://devdocs.io/javascript/global_objects/array/map) method to transform my `Array` of strings into an array of `Numbers`.  This will allow me to operate on the numbers. 

In order to get the list of operators from the expression, I use us `split` again, but this time I pass the regular expression (`\d`) as the `separator` parameter. I am basically telling `split` to build a new array using integers as the breaking point.  The result of which is passed to a [`Array.filter`](https://devdocs.io/javascript/global_objects/array/filter) so that I can clean up all of the blank array elements. 

At this point I should have everything I need to evaluate the expression passed into `calculate`. 

I'll use [`Array.forEach`](https://devdocs.io/javascript/global_objects/array/foreach) to perform an operation on each of the integers in the given expression.  Inside of the `forEach` callback method I'll grab the `operator` from the list of `operators` with one caveat.  I do not want to use the first operator on the first `number` from the `numbers` array. We'll perform the operations after the first number, so that we have an accurate result. 

Since the `operator` is of type `String` I cannot use that to calculate an expression (e.g. `1 + 1`), because the `+` will be treated as a string.  I'll use a `switch` statement and map the string `+` with the [Unary plus](https://devdocs.io/javascript/operators/arithmetic_operators#Unary_plus), and will do the same for the `-` with the [Subtraction](https://devdocs.io/javascript/operators/arithmetic_operators#Subtraction) operator. My `default` case assigns `result` to `number` since this will be the first number in the expression. 

That is about it, once we've iterated over all of the numbers in the expression, we return the result. 
