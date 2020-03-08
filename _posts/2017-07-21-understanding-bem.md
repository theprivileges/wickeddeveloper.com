---
title: Understanding BEM
description: A quick intro into BEM (Block Element Modifier) front-end methodology.
date: 2017-07-21 17:21:39
categories:
    - development
tags:
    - css
    - BEM
---

> This post was originally written for the enotes.com engineering blog.

# Understanding BEM

BEM (Block Element Modifier) is a front-end methodology, created to help build succinct and better organized CSS code.

Let's look an example of code that uses _regular_ class names, and compare it to code that uses BEM.

```html
<!-- non BEM -->
<form class="search" action="/">
  <label for="search-box" class="label required">Search</label>
  <input class="input" id="search-box" type="search" placeholder="What are you looking for?">
  <input class="button icon" type="submit" value="Search">
</form>
```

```html
<!-- BEM -->
<form class="search" action="/">
  <label for="search-box" class="search__label search__label--required">Search</label>
  <input class="search__input" id="search-box" type="search" placeholder="What are you looking for?">
  <input class="search__button search__button--icon" type="submit" value="Search">
</form>
```

Although the BEM markup looks similar, and perhaps a little longer with the class names, the advantages become more obvious when we compare the CSS for each example.

```css
/* non BEM */

.search {
  margin: 0;
  padding: 0;
  ...
}

/* specificity 0.0.2.0 */
.search .label {
  font-size: 14px;
  color: #CCC;
  ...
}

/* specificity 0.0.3.0 */
.search .label.required {
  color: #FF0000;
  ...
}

/* specificity 0.0.2.0 */
.search .input {
  padding: 5px 10px;
  font-size: 18px;
  ...
}
/* specificity 0.0.2.0 */
.search .button {
  font-size: 18px;
  ...
}

```

```css
/* BEM */

/* specificity 0.0.1.0 */
.search {
  margin: 0;
  padding: 0;
  ...
}

/* specificity 0.0.1.0 */
.search__label {
  font-size: 14px;
  color: #CCC;
  ...
}

/* specificity 0.0.1.0 */
.search__label--required {
  color: #FF0000;
  ...
}

/* specificity 0.0.1.0 */
.search__input {
  padding: 5px 10px;
  font-size: 18px;
  ...
}
/* specificity 0.0.1.0 */
.search__button {
  font-size: 18px;
  ...
}

```

As you can see, we've removed complexity, and reduced the [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) of our selectors, by rewriting our descendant selectors as simple selectors. This speeds up the time it takes for the browser to locate all of the targeted elements on the document.

Now let's look at the different parts of BEM.     

## Block

A __block__ is a self-contained entity on the page. Keep in mind that blocks can be compound, in which blocks have other blocks in them. (e.g: A navigation block inside of a header block.)

Say we want to create a `<figure>` which displays an image on the page. We create the `.avatar` block and apply that class to the html element that represents that block.  

```html
<figure>
  <div class="avatar">
    <img src="https://www.enotes.com/images/logos/logo-icon.jpg" alt="eNotes.com Logo">
  </div>
</figure>
```

```css
.avatar {
    margin: 0;
    padding: 0;
}
```

## Element

An __element__ is an individual piece of a __block__.  They make no sense on their own, and are tied to a __block__.  In the following example, we add an `img` element to the `.avatar` __block__.   We call it `.avatar__image`, and apply that class to the `img`.  This reduces the specificity of the selector, and allows us to target the element on the page a lot faster.  

```html
<figure>
  <div class="avatar">
    <img class="avatar__image" src="https://www.enotes.com/images/logos/logo-icon.jpg" alt="eNotes.com Logo">
  </div>
</figure>
```

```css
.avatar {
    margin: 0;
    padding: 0;
}

.avatar__image {
    width: 50px;
    height: 50px;
}
```

## Modifier

A __modifier__ changes or describes a __block__ or an __element__.
In the following example, we want the `.avatar__image` element to display a rounded image, by applying a `border-radius: 50%` to that element.  We create the `.avatar__image--rounded` modifier class, and apply it to the `img` element.  Now, we can tell right away that we are dealing with a rounded image.   

```html
<figure>
  <div class="avatar">
    <img class="avatar__image avatar__image--rounded" src="https://www.enotes.com/images/logos/logo-icon.jpg" alt="eNotes.com Logo">
  </div>
</figure>
```

```css
.avatar {
    margin: 0;
    padding: 0;
}

.avatar__image {
    width: 50px;
    height: 50px;
}

.avatar__image--rounded {
    border-radius: 50%;
}
```

That is pretty much the gist of BEM.  Now, let's look at a few recommendations.

## Recommendations

The following are some helpful recommendations to solve some common issues I ran into while learning about BEM.

### Do not use html elements as selectors

BEM can sort of provide us with a _scope_ by using unique class names.  If you start using HTML elements in your selectors, you'll be missing out on one of the benefits of BEM. Not only that but you can also fall prey to [directly targeted elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#Directly_targeted_elements_versus_inherited_styles), in which directly targeted elements will _always_ take precedence over inherited styles.

### Applying Modifier

You have to apply both the __element__ class and the __modifier__ class to the HTML element. Since the __modifier__ class has the same specificity as the __element__ class, we avoid inheritance conflicts.

```html
<ul class="menu">
  <li class="menu__item">Item 1</li>
  <li class="menu__item menu__item--gear">Item 2</li> <!-- correct -->
  <li class="menu__item--gear">Item 3</li> <!-- incorrect -->
</ul>
```

### Nested Components

BEM is not meant to communicate document structure.  When you are building the BEM tree, think in terms of composable components.


#### Block\__Element\__Element

If you find yourself writing classes that end up looking like `.edit-account-profile__form__label`, this should indicate to you that you may have to rethink your BEM tree.

```html
<div "edit-account-profile">
  <form class="edit-account-profile__form">
    <label class="edit-account-profile__form__label" for="account-name">Name</label> <!-- element element 😕 -->
    <input id="account-name" class="edit-account-profile__form__input" type="text" name="name" placeholder="What does your mamma call you?">
    <input class="edit-account-profile__form__save" type="submit" name="save" value="Save">
  </form>
</div>
```

To solve this use the __block__  in which the __element__ is a part of as your selector (e.g. `.edit-account-profile__label`.)

```html
<div "edit-account-profile">
  <form class="edit-account-profile__form">
    <label class="edit-account-profile__label" for="account-name">Name</label>
    <input id="account-name" class="edit-account-profile__input" type="text" name="name" placeholder="What does your mamma call you?">
    <input class="edit-account-profile__save" type="submit" name="save" value="Save">
  </form>
</div>
```

#### Element to Block

Sometimes an __element__ is really a self contained entity. Since a __block__ can be compounded, you can alleviate issues with nested components, by changing the __element__ into a new __block__ that composes the parent __block__.

```html
<ul class="menu">
  <li class="menu__item">Item 1</li>
  <li class="menu__item">Item 2</li>
  <li class="menu__item">
    <!-- search block composes menu block -->
    <form class="search" action="/">
      <label for="search-box" class="search__label">Search</label>
      <input class="search__input" id="search-box" type="search" placeholder="What are you looking for?">
      <input class="search__button" type="submit" value="Search">
    </form>
  </li>
</ul>
```

## Conclusion

BEM helps us solve a lot of issues related to specificity and css structure.  It helps avoid inheritance issues, and reduces conflicts in long living projects.  It may take a little getting used to at first, but, it will pay you dividends when you start moving entities on the page.  You and your team members will be able to quickly ascertain how entities on the page are related, and add to them with little to no friction.

## Acknowledgements

Thanks to [@nicholascloud](https://twitter.com/nicholascloud), [@mfonda](https://github.com/mfonda), and [@meganos](https://github.com/meganos) for reading a draft of this article.

## Resources

- [MindBEMding – getting your head ’round BEM syntax](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
- ['Why BEM?' in a nutshell](https://blog.decaf.de/2015/06/24/why-bem-in-a-nutshell/)
- [BEM by Example](https://seesparkbox.com/foundry/bem_by_example)
- [BEM](https://en.bem.info/)