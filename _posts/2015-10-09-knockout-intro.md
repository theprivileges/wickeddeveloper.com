---
title: Intro to Knockout Observables
description: A quick introduction to Knockout.js's observables.
date: 2015-10-09 18:25:31
tags:
    - knockout
    - javascript
    - tutorial
categories:
    - development
---

> This post was originally written for [modernweb.com](http://modernweb.com) but never published.

## Introduction

Today we'll be talking about Knockout observables and explicitly subscribing to observables. [Knockout](https://knockoutjs.com/) is a JavaScript library that helps us create rich applications that work seamlessly between the data model, and the UI.

## Obserables

[Observables](https://knockoutjs.com/documentation/observables.html) are an easy way to have two-way data binding.  Changes to the model layer are automatically displayed onto the UI, and vise-versa. As indicated in the Knockout documentation, observable objects are actually functions.  This is because of backwards compatibility, in older browsers [ES5 getters and setters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Defining_getters_and_setters) would not work, and that is why in Knockout, observables are functions.

```javascript
var viewModel = {
    // Set observable by passing argument to function
    name = ko.observable("Ryan")
};

// Get value of observable by calling function without parameters
console.log(viewModel.name());
```

### Turning it on

Borrowing from the example view model in the knockout [documentation](https://knockoutjs.com/documentation/introduction.html). You simply declare your model properties as observables.

```javascript
var viewModel = {
    userName: ko.observable("Bob"),
    userPermission: ko.observableArray(["read", "write"])
};

...

ko.applyBindings(viewModel);
```

With this in place you can apply the bindings to your UI, and any changes to the model will be reflected onto the UI, and any other dependencies.

```html
<p>Currently logged in as <span data-bind="text: userName"></span></p>
```

## Subscribing to observables

A common feature on the web is selecting a desired profile, from a list of available profiles. If in the process of selecting the appropriate profile we need to make an API call to an endpoint that fetches the profile's permission; then using an explicit subscription would be a good solution.

```javascript
// subscribing to changes on the userName
viewModel.userName.subscribe(function (newUserName) {
    // Call an endpoint with the new username and apply the permissions
    var request = new XMLHttpRequest();
    var endpoint = encodeURIComponent("/api/permissions/" + newUserName);
    request.onload = onGetPermissionsDone;
    request.open("GET", endpoint, true);
    request.send();
});
```
Creating these subscriptions ensures that all dependencies of the `userName` property in the model, are handled whenever its' value changes. Allowing me to trust that anything that cares about the value of `userName` is reacting appropriately, and in their own way.

### Terminating a subscription

In the event that you no longer want to be notified of any changes to the value of an observable, you can store the return value as a variable and call the `dispose` method on the result.

```javascript
var subscription = viewModel.userName.subscribe(function (newValue) { ... });
subscription.dispose();
```

These are great when writing unit tests for projects that use Knockout, as you can add your assertions inside of the callback function and call `dispose`, so as to not cause any issues with subsequent tests.

```javascript
describe("viewModel test", function () {
    describe("Changing username", function () {
        it("Should update the userName observable", function () {
            var newUserName = "Mike";
            var subscription = viewModel.userName.subscribe(function (newValue) {
                assert.equal(newValue, newUserName, "username is updated");
                subscription.dispose();
            });
            viewModel.userName(newUserName);
        });
    });
});
```

## Closing

We have only began to scratch the surface of what is possible with Knockout. I have found it to be easy to pickup and start coding with.  Can it be used any project? Probably, but it might not be the best solution in certain cases. Another great feature of Knockout observables are [Computed Observables](https://knockoutjs.com/documentation/computedObservables.html), which I hope to touch upon in another article. If you have used Knockout on a recent project, let me know what you think of it. 