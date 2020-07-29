---
layout: single
title: Library vs Framework
description: What is the difference between a library and a framework? The short answer
  is called inversion of control.
header:
  overlay_image: assets/images/development/header.jpg
  caption: Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [Unsplash](https://unsplash.com/s/photos/staring-at-laptop?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  show_overlay_excerpt: false
category:
- development
tags:
- concepts
- library
- framework
- jquery
- react
- vue
- inversion of control
classes: wide
date: '2020-07-29 00:28:39 +0000'
---
# What is the difference between a Library and a Framework? 

The simple answer comes from a the concept called **Inversion of Control**, sometimes referred to as the _Hollywood Principle_. 

Generally speaking a library provides you with functions that you call yourself.  You as the developer are in control, you decide when to call the functions. A framework will execute your functions for you, it controls when your code gets executed — control is inverted.

## Library

A popular library in the JavaScript ecosystem is [jQuery](https://jquery.com/) which provides us with a number of methods (e.g. [`on`](https://api.jquery.com/on/)) that we can use to manipulate the DOM, attach callback handlers, etc. As you write your code using jQuery, you are in control of when and how your functions get executed.

```js
function handler () {
    console.log("button clicked");
}

$("button").on("click", handler);
```

In the above example we control when `handler` gets called, whenever the `button` element gets clicked. 

## Framework

Frameworks on the other hand are responsible for calling your code. Frameworks like [React](https://reactjs.org/) and [Vue.js](https://vuejs.org/) provide you with a set of instructions on how to write your code such that it can be called on by the framework themselves. 

> One important characteristic of a framework is that the methods defined by the user to tailor the framework will often be called from within the framework itself, rather than from the user's application code. The framework often plays the role of the main program in coordinating and sequencing application activity. This inversion of control gives frameworks the power to serve as extensible skeletons. The methods supplied by the user tailor the generic algorithms defined in the framework for a particular application. <br/>
—— [Ralph Johnson and Brian Foote](http://www.laputan.org/drc/drc.html)

Let's look an example with React.  The following is just a functional component that displays the status of an user.  It uses the [`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect) hook to subscribe and unsubscribe to an API that checks the status of an user.  You write the code but the framework calls it during its' reconciliation phase.

```js
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    // this is called by the framework
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      // this is also called by the framework
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

## Summary

- Inversion of Control is a key characteristic of a framework.
- In a library you are in control of when your code gets executed and how it gets executed.
- In a framework your code is executed by the framework, you build functionality that you would like the framework to execute given certain constraints.
- Inversion of Control is also referred to as the _Hollywood Principle_.

## Resources

- [InversionOfControl](https://martinfowler.com/bliki/InversionOfControl.html)