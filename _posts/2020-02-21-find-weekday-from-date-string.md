---
title: Use Intl.DateTimeFormat To Find Weekday From a Given Date String
description: Use the Intl.DateTimeFormat constructor, to find the weekday of a given date string.
tags: tutorial, javascript, beginners, i18n
cover_image: https://thepracticaldev.s3.amazonaws.com/i/xrnkvy42s5n1snu7htgb.jpeg
---

I've recently been introduced to the `Intl` object, which is used as the namespace for the [ECMAScript Internationalization API](https://norbertlindenberg.com/2012/12/ecmascript-internationalization-api/index.html).  It has a neat object called `DateTimeFormat` which can be used to format a date value into locale specific strings. 

I'll show you a typical use case for using `Intl.DateTimeFormat` to generate the weekday of a given date string (e.g. `07/16/1945`).

## Problem

Given a `dateString` in the format `MM/DD/YYYY`, find and return the weekday for that date.  

## Solution

```js
/**
 * Given a date string in the format MM/DD/YYY, find and return the 
 * weekday for that date in English.
 *
 * @param {string} dateString
 * @returns {string} - weekday for the given date [e.g: Wednesday]
 */
const getWeekDay = (dateString) => {
  const date = new Date(dateString);
  const dateTimeFormatOptions = { weekday: 'long' };
  const dateTimeFormat = new Intl.DateTimeFormat('en-US', dateTimeFormatOptions); 
  return dateTimeFormat.format(date);
}
```

## Explanation

1. Create a function expression called `getWeekDay` which takes a string (`dateString`).
2. Create a `Date` object with the given `dateString`, so that we can pass it as a parameter into the `format` method of `DateTimeFormat`.
3. Create an object to hold the [`options`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat#Parameters) parameter for `Intl.DateTimeFormat`. Setting the `weekday` property equals to `long`, so that we get the localized weekday when calling `format`.
4. Create a an instance of [`Intl.DateTimeFormat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat) setting `locales` to `en-US`, and passing in the previously created `dateTimeFormatOptions` object.
5. Return the result of calling [`format`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat/format) method on `Intl.DateTimeFormat` to find the weekday for the given `date`. 

## Output

```js
console.log(getWeekDay("07/16/1945"));
// expected output: "Monday"

```

In closing, we used the `Intl.DateTimeFormat` object to quickly find the weekday of a given date string. Best of all [`Intl`](https://caniuse.com/#feat=internationalization) has great support across modern browser. 

Thank you for reading. 

> Originally posted at [dev.to](https://dev.to/theprivileges/easy-way-to-find-weekday-from-a-given-date-string-le6)
