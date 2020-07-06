---
layout: single
title: JavaScript Custom Events
description: A quick look at how to use JavaScript CustomEvent object to create and
  consume custom events, so that different parts of an application can communicate
  with one another.
header:
  overlay_filter: rgba(0, 0, 0, 0.6)
  overlay_image: assets/images/tutorial/header.jpg
  caption: Photo by [Roozbeh Eslami](https://unsplash.com/@roozbeheslami?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  show_overlay_excerpt: false
category:
- development
tags:
- javascript
- tutorial
date: '2020-07-06 23:32:53 +0000'
---
Modern web applications rely a lot on JavaScript, and different elements on a page may need to communicate with other elements.  What happens if those elements are rendered by separate codebases, how would you "connect" them? A valid solution could be found in [`CustomEvent`](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events#Creating_custom_events).  This API allows us to create our own events that pass the data we need, and we can use [`addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) throughout our app in order to execute some piece of code based on our custom event. 

### `CustomEvent`

The `CustomEvent` API is fairly straight forward: 

```js
const item = 'book'
const customItemSelectedEvent = new CustomEvent(
    'custom:item-selected', 
    { 
        detail: { 
            item 
        }
    })
```

In the code above we create a custom event with the name `custom:item-selected`.  I generally like to namespace my events following a `:` so as to not cause any conflicts with any other 3rd party library. We are passing an `item` property in the [`detail`](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent/detail) property so that any consuming listener may have access to the value of `item`.  One use case for this is when `item` is something that the enduser controls, say a list of items displayed on the page. 

### `dispatchEvent`

Once our `customItemSelectedEvent` is created, we need to fire it.  Firing a custom event is as simple as attaching it to an `HTMLElement` and calling the [`dispatchEvent`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/dispatchEvent) method on that `HTMLElement`. 

```js
const item = 'book'
const customItemSelectedEvent = new CustomEvent(
    'custom:item-selected', 
    { 
        detail: { 
            item 
        }
    })

const el = document.querySelector('.items')

el.dispatchEvent(customItemSelectedEvent)
```

In the example above we dispatch our `customItemSelectedEvent` on a hypothetical `HTMLElement` with a css class named `items`.

### `addEventListener`

Consuming a custom event is no different than consuming any other `Event`.  We simply add a listener on the `HTMLElement` that we trigerred the `CustomEvent` on, in our case `.items`. 

```js
// some other file

const el = document.querySelector('.items')
el.addEventListener('custom:item-selected', (e) => {
    console.debug('Selected Item:', e.detail)
})

```

That is pretty much it, those are the steps for creating your custom event.  I've used this pattern whenever building a custom library for a project, or whenever an application I am working in has two separate codebases (e.g. legacy JavaScript files using bootstrap, and new files using React.)  