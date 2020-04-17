---
title: A case for expression reduction
description: A case for assigning complex condition statements to a variable, so that
  your code becomes easier to grok.
header:
  overlay_color: "#333"
  show_overlay_excerpt: false
category:
- development
tags:
- javascript
- opinion
---
As a software developer you will inevitably have to debug some piece of code you wrote months if not years ago, or code from a colleague that is no longer part of your team.  As you step through some routine you notice an array of conditional statements with complicated conditional expressions. As you search for the bug in the code you'll end up noticing that you can't hold all of the values in your head.  You can no longer remember what a particular value means or what it points to. 

I have found that creating boolean variables that hold the value of an expensive or complicated expression makes it easier to read and understand code. 

Let's look at a trivial piece of code, and see how assigning complex conditions to a variable makes it much easier to understand and read the code. _Keep in mind this code is not something you'd use in production, I'm only using this to illustrate the point._

Suppose there is a `function` that takes an argument called `drink` and inside of this function we check what type of drink it is and return an emoji of a coffee, tea, or milk. 

```js
function getDrinkEmoji(drink) {
    if (drink === COFFEE || drink === CAFE || drink === LATE || drink === MOCHA) {
        return '☕';
    } else if (drink === TEA || drink === BLACK_TEA || drink === GREEN_TEA || drink === OOLONG_TEA) {
        return '🍵';
    } else {
        return '🥛';
    }
}
```

Reading through code like that requires you to hold quite a lot in your head.

Now let's look at the same code but having assigned the expression to a variable.

```js
function getDrinkEmoji(drink) {
    const isCoffee = drink === COFFEE || drink === CAFE || drink === LATE || drink === MOCHA;
    const isTea = drink === TEA || drink === BLACK_TEA || drink === GREEN_TEA || drink === OOLONG_TEA;

    if (isCoffee) {
        return '☕';
    } else if (isTea) {
        return '🍵';
    } else {
        return '🥛';
    }
}
```

Here we can more quickly understand what the expressions inside of the `if` and `else if` are evaluating to.

<div class="notice--info">
:pushpin: You may also prefix your variables with words like <code>has</code>, <code>should</code>, <code>was</code>, etc.
</div>

This pattern makes a lot of sense when you find yourself evaluating the condition multiple times.  When you do it once you can just reference the variable again when you need it. 

In this next example, our `function` receives an array of `drinks`, we use the [`Array.some`](https://devdocs.io/javascript/global_objects/array/some) method to test whether the `drinks` include a coffee or a tea and then return an emoji.

```js
function getDrinksEmoji(drinks) {
    const hasCoffee = drinks.some(drink => drink === COFFEE || drink === CAFE || drink === LATE || drink === MOCHA);
    const hasTea = drinks.some(drink => drink === TEA || drink === BLACK_TEA || drink === GREEN_TEA || drink === OOLONG_TEA);
    const hasCoffeeAndTea = hasCoffee && hasTea;

    if (hasCoffeeAndTea) {
        return '☕ + 🍵';
    } else if (hasCoffee) {
        return '☕';
    } else if (hasTea) {
        return '🍵';
    } else {
        return '🥛';
    }
}
```

We had to execute the expensive computation of testing if the `drinks` include a coffee or tea once, we referenced that expression multiple times in our code without additional performance penalty, and the code is still easy to read and understand.


## Conclusion

Conditional statements are an invaluable tools in software development, they provide us with flow control to determine the output of our programs.  You'll inevitably run across them when writing and reading code.  If you are the author of the code, or reading code that you have control over, do yourself a favor and assign your expensive and complicated condition statements to variables with meaningful names.  Doing so will free up space in your head and your code will be much easier to read and understand. 

## Links

- [JavaScript — Conditional Operators](https://javascript.info/ifelse)
- [Conditional (computer programming)](https://en.wikipedia.org/wiki/Conditional_(computer_programming))
- [How To Write Conditional Statements in JavaScript](https://www.digitalocean.com/community/tutorials/how-to-write-conditional-statements-in-javascript)
- [Conditional Execution in C++](https://cal-linux.com/tutorials/conditionals.html)
- [Predicate (mathematical logic)](https://en.wikipedia.org/wiki/Predicate_%28mathematical_logic%29)

---

__Thanks__ to @nicholascloud for reading a draft of this post, and for giving this pattern a name (_expression reduction_).