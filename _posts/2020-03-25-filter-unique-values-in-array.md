---
title: Filtering unique values in an array
description: Use Array.filter to generate a new array of unique values from a source array.
date: 2020-03-24 18:07 +0700
header:
  overlay_filter: "rgba(0, 0, 0, 0.6)"
  overlay_image: assets/images/tutorial/header.jpg
  caption: "Photo by [Roozbeh Eslami](https://unsplash.com/@roozbeheslami?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  show_overlay_excerpt: false
category:
  - development
tags:
  - javascript
  - tutorial
---

Here is a quick and easy way to filter all unique values from an array using the [`Array.filter`](https://devdocs.io/javascript/global_objects/array/filter) and [`Array.indexOf`](https://devdocs.io/javascript/global_objects/array/indexof) methods.

## Explanation

The `Array.filter` method returns a new array containing all elements that pass a predicate. With that in mind we can use the `Array.indexOf` method, which returns the first index at which a given element can be found in the array, inside of the predicate in order to test whether or not the current index is the same as the first index of the element we are iterating on. 

Since `Array.filter`'s callback accepts three arguments (`element`, `index`, `array`) we'll use these values to make our predicate return `true` only if the current `element`'s index is the current `index`.


## Example 

```js
const sample = ['_conf.scss', '_mixin.scss', '_mixin.scss', '_mixin.scss', 'main.scss'];

// Return true when the indexOf(element) is the current index, otherwise we've seen element already.
const filtered = sample.filter((element, index, array) => array.indexOf(element) === index);
// => ['_conf.scss', '_mixin.scss', 'main.scss']
```

[Try it](https://jsbin.com/duluyon/edit?js,console)