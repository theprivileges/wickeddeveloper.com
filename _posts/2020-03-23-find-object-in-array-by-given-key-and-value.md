---
title: Find object in array by given key and value
description: An example of how to use Array.filter to search for elements in a collection by a given key and value.
date: 2020-03-22 18:00 +0700
header:
    overlay_color: "#333"
    show_overlay_excerpt: false
category:
    - development
tags:
    - javascript
    - tutorial
---

At my current job we work a lot with collections, and one of the operations we run is pulling certain items from the collection based on some combination of a key,value.  This was happening so much throughout the code that I've decided to write my own util function to return a new collection which included only the items I am interested in.

## Function

```js
/**
 * Given a property and value find all matches in an array of objects
 * @param {Array} arr collection to be searched
 * @param {String} prop name of property we are searching for
 * @param {*} value the value of the specified property we are searching for
 * @returns {Array} array with elements that match value for the given property
 */
const searchInArray = (arr, prop, value) => arr.filter(element => element[prop] === value);
```

### Explanation

The `searchInArray` method takes three arguments: (`arr`, `prop`, `value`). It uses [`Array.filter`](https://devdocs.io/javascript/global_objects/array/filter) to test each element in the collection and returns the matched elements.

The callback to `Array.filter` looks at the value of the given `prop` and tests it againt the `value` we are looking for. The element that pass the test are returned as a new array.

## Use

Suppose we have a list of ids (e.g. `selected`) that we are looking for in a collection (e.g. `labels`), and we want to return only those elements that match the given ids.

```js
// dummy collection
const labels = [
    { id: 1, name:"string 1", value:"this", other: "that" },
    { id: 2, name:"string 2", value:"this", other: "that" },
    { id: 3, name:"string 2", value:"this", other: "that" },
];

// list of ids we want
const selected = [1,3];
```

We can use the [`Array.flatMap`](https://devdocs.io/javascript/global_objects/array/flatmap) method on the `selected` list, and use our `searchInArray` method as the callback to `Array.flatMap`, creating a new list of elements of which we are looking for.

```js
const result = selected.flatMap(id => searchInArray(labels, 'id', id));
// [{ id: 1, name:"string 1", value:"this", other: "that" }, { id: 3, name:"string 2", value:"this", other: "that" }]
```


## Demo

[JS Bin](https://jsbin.com/nohuzow/edit?js,console)