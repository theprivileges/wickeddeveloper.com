---
layout: single
title: Code Splitting React Application with Loadable Components
---

As your React application grows, most of us end up with large bundles, especially if we are importing large 3rd-party dependencies.  In order to keep our bundle sizes at a manageable size we can leverage code-splitting technique available to use using webpack.  I'll show you how to implement code-splitting in an existing React application that is bundled using webpack using Loadable Components.

## Code-Splitting

Code-Splitting is a compeling feature of webpack, which allows you to "split" your code into smaller bundles called "chunks" which can be loaded in parallel or on demand. It is one of those features that if done correctly can significantly improve the performance of your application.

## Code-Splitting and React

Once you have configured webpack to handle code-splitting, you can start working on splitting your React application.  Most people start this process by doing what is called [route based code-splitting](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting).

### Route Based Code-Splitting

The easiest way to start breaking your bundles into smaller "chunks" is by [dynamically importing]() components based on routes.  This will allow us to only request a component when we know that our end-user is going to need that file.  Since most people on the web today are used to navigating to a page and waiting some amount of time before the page is loaded, we can take advantage of this learned behavior. 

The default way to implement code-splitting in React is done using `React.Suspense` and `React.lazy`.  Combined these two features allows us to dynamically import a component using `React.lazy` and to display a `fallback` while that component has not been fully loaded yet. Most developers can survive using those built-in features.  However, some of us have slightly more complex applications that require a bit more.

### Loadable Components

Loadable Components is a module that turns `React.Suspense` and `React.lazy` up to [11](https://loadable-components.com/docs/loadable-vs-react-lazy/).  

## Summary

As your React application grows in size, your bundles are going to get bigger.  Most of the time you do not want to ship all of that code to your end-user. Code-Splitting is a technique that you can use to break your bundles into smaller "chunks" that can by dynamically imported when the end-user is ready to execute that code. Code-Splitting is one of the most compeling features of webpack, and when done correctly can significantly improve the performance of your application. Configuring wepback to handle code-splitting is fairly straight forward, and React ships with built-in code-splitting feature. If you are not satisfied with these built-in features a good alternative is Loadable Components which allows us to dynamically import components with or without `React.Suspense`, and we can also code-split libraries.  Combined all of these features allows us to serve only the necessary code to our end-user, making our application perform better, and decreasing bundle sizes.


## Resources

- [Webpack Guide to Code-Splitting](https://webpack.js.org/guides/code-splitting/)
- [React Guide to Code-Splitting](https://reactjs.org/docs/code-splitting.html#code-splitting)
- [Loadable Components](https://webpack.js.org/guides/code-splitting/)
- [`@babel/plugin-syntax-dynamic-import`](https://babeljs.io/docs/en/babel-plugin-syntax-dynamic-import/#installation)>