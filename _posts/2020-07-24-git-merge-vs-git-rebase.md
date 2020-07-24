---
layout: single
title: Git Merge vs Git Rebase
description: A quick review of the differences between git rebase and git merge, and
  recommendations on when to use them.
date: '2020-07-24 02:31:53 +0000'
header:
  overlay_filter: rgba(0, 0, 0, 0.6)
  overlay_image: assets/images/tutorial/header.jpg
  caption: Photo by [Roozbeh Eslami](https://unsplash.com/@roozbeheslami?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  show_overlay_excerpt: false
category:
- development
tags:
- git
- workflow
---
> What is the differenct between `git merge` and `git rebase`? 

Over the years I've been asked this question by several people, either during an interview or by a less experienced developer on the team. 

Atlassian's [Merging Vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) article does a fantastic job at explaining the differences and when to incorporate `git rebase` into a development workflow.  However, I wanted to recount that lesson in my own words, and that is what I hope to do in this post. 

## First things first

Both `git merge` and `git rebase` are commands you would use to integrate changes from one branch into another branch.  The main difference is that `git merge` will create a new commit in the commit history, whereas `git rebase` will not. 

## Merge Option

Merging is the safest way to integrate changes from one branch into another branch, however it will create a new commit called "merge commit" which will tie the history of both branches together. 

Running `git merge feature master` would result in a structure that looks like this: 

<img alt="Merging the feature branch onto master" src="/assets/images/git/merge.svg"/>

Merging does not re-write history or changes the existing branches, this is why it is considered to be a _non-destructive_ operation.

The one caveat with `git merge` is that while you are working on your feature, `master` can be updated with changes that you would want to incorporate into your `feature` branch. Every `git merge` command you execute will create a new "merge commit".  This is why some people prefer to use `git rebase`. 

## Rebase Option

Rebasing solves the same problem as merging, but it does so by re-writing the commit history of the `feature` branch. It accomplishes that by re-applying the changes in the `feature` branch onto the tip of the `master` branch. 

```sh
git checkout feature
git rebase master
```

<img alt="Rebasing the feature branch onto master" src="/assets/images/git/rebase.svg"/>

As you can see this results in a much cleaner commit history, we no longer have the "merge commit" from `git merge`.  However, there are trade-offs. 

- You no longer have a history of when changes from `master` were integrated into the `feature`. 
- You are prevented from pushing these changes to a remote origin if that remote origin has been changed by another user.

In order to avoid the second trade-off, your team must follow **The Golder Rule of Rebasing**.

## The Golden Rule of Rebasing

You do not want to run `git rebase` on a branch that has been pushed to a remote origin where it has been worked on by more than one person.  This will cause you much pain, since `git rebase` will re-write the commit history of that branch. 

> “Is anyone else looking at this branch?” If the answer is yes, take your hands off the keyboard and start thinking about a non-destructive way to make your changes

## Summary

- `git rebase` and `git merge` are two ways of performing the same task of integrating changes from one branch into another.
- `git merge` is the safest and easiest way to accomplish that task.
- `git merge` will create a new "merge commit", which can create noise in the commit history.
- `git rebase` can be used to keep a cleaner commit history, but it comes with trade-offs.
- Your team must follow **The Golder Rule of Rebasing** if you are going to be using `git rebase` in your workflow.
- **DO NOT** execute `git rebase` on a branch that has been made public, especially if others have contributed to that branch.

> If you get stuck there is always [oh Shit, Git!?!](https://ohshitgit.com/)

## Resources

- [Atlassian Merging Vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

## License

This page has borrowed some of the images of the [Atlassian Merging Vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) article which are licensed under [CC BY 2.5 AU](https://creativecommons.org/licenses/by/2.5/au/).