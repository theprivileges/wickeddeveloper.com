---
layout: single
title: JavaScript Custom Events
---

# JavaScript Custom Events

When building modern web applications they rely a lot on JavaScript, and different elements on the page may need to communicate with other element.  This is when `CustomEvent` API comes in.  This API allows us to create our own events that pass the data we need, and we can use `addEventListener` throughout the app in order to execute some piece of code based on our custom event. 

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

In the code above we create a custom event with the name `custom:item-selected`.  I generally like to namespace my events following a `:` so as to not cause any conflicts with any other 3rd party library. We are passing an `item` property in the `detail` property so that any consuming listener may have access to the value of `item`.  One use case for this is when `item` is something that the enduser controls, say a list of items displayed on the page. 

Once our `customItemSelectedEvent` is created, we need to fire it.  Firing a custom event is as simple as attaching it to an `HTMLElement` and calling the `dispatchEvent` method. 

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

In the example above we dispatch our `customItemSelectedEvent` on a hypothetical `HTMLElement` that has a call of `.items`.

Consuming a custom event is no different than consuming any other `Event`.  We simply add a listener on the `HTMLElement` that we trigerred the `CustomEvent` on, in our case `.items`. 

```js
// some other file

const el = document.querySelector('.items')
el.addEventListener('custom:item-selected', (e) => {
    console.debug('Selected Item:', e.detail)
})

```

That is pretty much it, those are the steps for creating your custom event.  I've used this pattern whenever building a custom library for a project, or whenever an application I am working in has two separate codebases (e.g. legacy JavaScript files using bootstrap, and new files using React.)  