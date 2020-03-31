---
title: How I Manage My ZSH Plugins
description: using zplug to manage my zsh plugins
date: 2020-03-30 22:00 +0700
header:
  overlay_filter: "rgba(0, 0, 0, 0.6)"
  overlay_image: assets/images/tutorial/header.jpg
  caption: "Photo by [Roozbeh Eslami](https://unsplash.com/@roozbeheslami?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  show_overlay_excerpt: false
category:
  - development
tags:
  - tutorial
  - setup
  - zsh
---

I am a big fan of [`zsh`](https://en.wikipedia.org/wiki/Z_shell), so much so that part of my [setup script](https://github.com/theprivileges/shared-dotfiles/blob/62a21d589b5dca595096757b70819161dcb86432/tag-mac/bootstrap#L42) contains instructions to install it and set it as the default shell. 

One of the biggest advantages of using `zsh` are the plugins and functions that you can use to amplify your terminal powers.  I've been using [`oh-my-zsh`](https://ohmyz.sh/) to manage my `zsh` configuration, and recently I started using [`zplug`](https://github.com/zplug/zplug) to manage all of the plugins and customizations I use.

## A next-generation plugin manager for zsh

`zplug` offers an intuitive and fast way to manage everything I rely on when using `zsh`. I've gone so far as to use it as the main form of loading plugins and other customizations for `zsh`. I'll show you a brief overview of how I manage the plugins I use.

## Installing

You can install `zplug` by running the following [script](https://github.com/zplug/installer/blob/master/installer.zsh).

```sh
curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh
```

## Configuring

Once installed I make sure to update my `.zshrc` with a `zplug` section that will load all of the necessary customizations I want.

### Loading oh-my-zsh plugins

I still borrow from the vast array of plugins and functions the `oh-my-zsh` community has provided to the world.

```sh
# Load oh-my-zsh plugins
zplug "plugins/brew",   from:oh-my-zsh
zplug "plugins/docker",   from:oh-my-zsh
zplug "plugins/docker-compose",   from:oh-my-zsh
zplug "plugins/git",   from:oh-my-zsh
zplug "plugins/github",   from:oh-my-zsh
zplug "plugins/osx",   from:oh-my-zsh
```

### Loading theme

I use the [dracula theme](https://draculatheme.com/zsh), and loading it is a simple as:

```sh
# Load theme file
zplug "dracula/zsh", as:theme
```

### Install Plugins

After adding the `zplug` section to my `.zshrc` I make sure to add the following to the end of that section, so that `zplug` makes certain to install all of the plugins I've specified.

```sh
# Install plugins if there are plugins that have not been installed
if ! zplug check --verbose; then
    printf "Install? [y/N]: "
    if read -q; then
        echo; zplug install
    fi
fi
```

### Source plugins

Finally, you can add the following so the plugins can be sourced and added to the `$PATH`

```sh
# Then, source plugins and add commands to $PATH
zplug load
```

## Links

- [Installing ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)
- [Installing zplug with Homebrew](https://github.com/zplug/zplug#using-homebrew-os-x)
- [brew plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/brew)
- [docker plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/docker)
- [docker-compose plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/docker-compose)
- [git plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git)
- [github plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/github)
- [osx plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/osx)