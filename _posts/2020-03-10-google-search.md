---
title: How I configure Google Search on the browser
categories:
    - privacy
tags:
    - setup
    - privacy
    - browser
---

One of the first things I do when I install a fresh version of a Web Browser, is change the Default Search Engine to [DuckDuckGo](https://start.duckduckgo.com).  I have been slowly moving towards owning my digital data, and have joined the [de-Google](https://degoogle.jmoore.dev/) movement. Unfortunatelly, sometimes I have to use Google for search.  

The following is how I configure [Brave Browser](https://brave.com/zos304) to use `google.de` instead of `google.com`.  I use `google.de` because of the [E.U Privacy Rules](https://www.nytimes.com/2014/05/14/technology/google-should-erase-web-links-to-some-personal-data-europes-highest-court-says.html). 

## Set Search Engine in Settings

- Launch Brave Browser
- Open the Menu <span class="fas fa-fw fa-bars" aria-hidden="true"></span>
- Navigate to **Settings** -> **Search Engines**
- Click on **Manage Search Engines**

## Manage Search Engines

After clicking on **Manage Search Engines**, you'll be presented with a large list of available search engines. What I usually do is set **DuckDuckGo** as my *Default Search Engine*, I also **Remove** the current configuration for **Google**. 

Next, I add a new version of **Google**.

## Adding Search Engines

- Click on the **Add** button.
    - **Search Engine**: `Google`
    - **Keyword**: `google`
    - **URL**: `https://www.google.de/search?q=%s&hl=en`
- Click on the **Add** button.

> the `hl=en` is the piece that tells Google to use English as the home language.

## Testing

Now you should be able to type `google` and hit `Space` or `Tab` and type your search phrase. When you hit `Enter` you should be taken to the Google results page in `google.de`.

## Conclusion

I have been working on de-Googling my life, but sometimes I end up using Google to search for something (e.g [Animated Gifs](https://bob.yexley.net/custom-animated-gif-search/)), but since I care about privacy, I end up removing the default Google setup on the browser and replacing it with a version that uses the European version of Google.  This allows me to use Google with a little extra privacy. It is not perfect, but it puts my mind at ease. 