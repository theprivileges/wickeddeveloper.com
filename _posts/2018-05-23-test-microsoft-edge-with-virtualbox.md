---
title: Microsoft Edge Legacy with VirtualBox
description: A quick-start guide for creating a windows virtual machine that you can use to test your code on Microsoft Edge Legacy.
date: 2018-05-23 15:15:16
categories:
    - development
tags:
    - virtualbox
    - microsoft
    - edge
    - guide
---

> This guide was originally written for enotes.com development setup

The following are the steps for downloading and running Microsoft Edge Legacy on VirtualBox.

# Step 1 — Download Virtual Box

Head to [`https://www.virtualbox.org/wiki/Downloads`](https://www.virtualbox.org/wiki/Downloads), and download the appropriate platform package.

# Step 2 — Download Virtual Machine

Microsoft's `modern.ie` has kindly provided us with images from IE8 to MSEdge.  You can download these images at [`https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/`](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/).

- Select the _MSEdge_ option under _Virtual Machine_.
- Select _VirtualBox_ under _Platform_.
- Click _Download .ZIP_.

# Step 3 — Extracting ZIP (optional)

The MSEdge virtual machine comes compressed inside a 7-zip file. Mac Archiver may not be able to extract this file.
You may download [The Unarchiver](https://theunarchiver.com/) in order to extract the image.

# Step 4 — Installing the Virtual Machine

- Double click on the .ova file.
- Once _VirtualBox_ is launched update the _RAM_ setting to at least _1GB_ if you can afford it.
- (optional) Create a snapshot of the Virtual Machine.  This will help when the 90 days of trial expires.

# Step 5 — Booting up

- Select the _MSEdge_ Virtual Machine.
- Click _Start_.
- Wait for Windows to boot.
- Once started, install _Guest Additions_
  - Click _Devices_ on the toolbar menu.
  - Select _Install Guest Additions_.
  - You may have to restart the Virtual Machine.
  
# Step 6 — :moneybag:

- Once started, you can use MSEdge to load up the website in question.
- MSEdge's developer tools is called [F12](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide).

## Links

- [MAKING INTERNET EXPLORER TESTING EASIER WITH NEW IE VMS](https://blog.reybango.com/2013/02/04/making-internet-explorer-testing-easier-with-new-ie-vms/)
- [Installing modern.ie Virtualization on VirtualBox for Mac](https://chriswharton.me/2013/02/installing-modern-ie-virtualization-on-virtualbox-for-mac/)