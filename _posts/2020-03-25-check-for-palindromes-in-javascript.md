---
title: Check for Palindromes in JavaScript
description: Using the built-in methods in JavaScript to test if a phrase is a palindrome.
date: 2020-03-25 18:45 +0700
header:
  overlay_image: assets/images/challenge/header.jpeg
  caption: "Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/hacker?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  show_overlay_excerpt: false
---

A palindrome is a word, phrase, number, or other sequence of characters which reads the same backwards as it does forward.

I've come across this challenge many times, so I've decided to post my default solution to this particular variation. 

## Problem

Design an function that, given a string, returns `true` if the string is a palindrome and `false` if it is not.

## Constraints

1. The string may contain spaces and punctuation, but they are not considered when detecting palindromeness. Just ignore them.
2. The string may contain numbers, but must contain at least one letter.
3. Consider all alphanumeric characters. The string must be the same backwards as it is normally.
4. When developing your algorithm, try to take performance into account.

## Solution

```js
function isPalindrome(phrase = '') {
  // must contain at least one letter.
  if (!/[A-Za-z]/i.test(phrase)) return false;
  
  const sanitized = phrase.replace(/\W/g, '') // strip spaces and punctuation
                          .toLowerCase();     // normalize
  const reverse = [...sanitized]              // break letters into array
                      .reverse()              // reverse letters
                      .join('');              // put it back into string
  return sanitized === reverse;
}
```

[Try it](https://jsbin.com/tolizej/edit?js,console)

### Breakdown

The function takes one argument `phrase` and it uses the [`RegEx.test`](https://devdocs.io/javascript/global_objects/regexp/test) method to make sure that we have at least one letter, per the requirements. 

Assuming we have a `phrase` that has at least `1` letter, I strip all spaces and punctuation from `phrase` using [`String.replace`](https://devdocs.io/javascript/global_objects/string/replace) with the regular expression (`\W`) which is equivalent to [`[^A-Za-z0–9_]`](https://en.wikipedia.org/wiki/Regular_expression#Character_classes). Next, we use [`String.toLowerCase`](https://devdocs.io/javascript/global_objects/string/tolowercase) to transform this sanitized string into its' lower case version.  This will facilitate the comparison with the original phrase.

After storing the normalized string (e.g. `sanitized`), I move on to reversing that string so that I can compare it with the "original". I use the [spread syntax](https://devdocs.io/javascript/operators/spread_syntax) to convert each letter into an array of letters.

> I do not use `String.split` because the string is not split between each user-perceived character ([grapheme cluster](https://unicode.org/reports/tr29/#Grapheme_Cluster_Boundaries)) or between each unicode character (codepoint) but between each UTF-16 codeunit.

Once I have every character in an array form, I can use the [`Array.reverse`](https://devdocs.io/javascript/global_objects/array/reverse) and [`Array.join`](https://devdocs.io/javascript/global_objects/array/join) methods to reverse the order of the characters and produce a string in reverse order.

Finally we can return the result of a condition that tests if the normalized version of `phrase` is equal to the reversed version of that normalized version.

## Link

[How do you get a string to a character array in JavaScript](https://stackoverflow.com/questions/4547609/how-do-you-get-a-string-to-a-character-array-in-javascript/34717402#34717402)