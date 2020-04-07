---
title: Alternatives to Zoom
description: Alternatives to Zoom video conferencing app for people who care about privacy and security.
date: 2020-04-06 20:47 +0700
categories:
  - privacy
tags:
  - privacy
  - video 
  - security
  - cybersecurity
  - webrtc
header:
  overlay_image: assets/images/meeting/header.jpg
  caption: "Photo by [dylan nolte](https://unsplash.com/@dylan_nolte?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/meeting?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
  show_overlay_excerpt: false
---

Over the past few weeks businesses and people have been scrambling to adjust to a work from home way of life.  People went searching for ways to communicate with colleagues and family over video calls.  A large number of these people resorted to using Zoom as their video conferencing application.  Unfortunately, [security researchers](https://www.forbes.com/sites/kateoflahertyuk/2020/04/04/new-zoom-user-blow-this-is-how-thousands-of-video-chats-are-available-for-anyone-to-view-online/#7dd5c381785d) have exposed many [flaws](https://theintercept.com/2020/04/03/zooms-encryption-is-not-suited-for-secrets-and-has-surprising-links-to-china-researchers-discover/) in Zoom's application(s). 

The following are some alternatives for those who value security and privacy.  These services use a web technology called WebRTC, which provides peer-to-peer encryption out of the box. If your team or group of friends is small you can use the following alternatives without sending sensitive information to a server.  Once you exceed a certain number of participants different services will begin to route traffic through a server. 

## Daily.co

[Daily.co](https://daily.co) offers easy, flexible in-browser video calls that run in your web browser. There is no software to download. When you sign up for their free plan, you can start calls on the browser with up to 50 participants.  When there are 4 or fewer people on the call all traffic is routed between the participants.  Once more participants join the call, there are bandwidth limitations which causes the services to switch from p2p to relayed connections. It first tries to send UDP traffic through their servers, if that fails it switches to TCP-tunneling, while preserving encryption to and from the server

You can read more about how daily.co handles privacy in this [post](https://help.daily.co/en/articles/1189715-peer-to-peer-vs-cloud-meetings-bandwidth-privacy-and-architecture). 

## Whereby

[Whereby](https://whereby.com/) is another service that offers in-browser video calls. Their free version can support up to 4 participants, and you have access to 1 meeting room.  They are a European company and might be a better option for those in the E.U. It does seem like chat messages do pass through their servers before reaching the other participants. 

Read more about their data storage and security [here](https://whereby.helpscoutdocs.com/article/334-data-storage-security). 

## Jitsi

For those of us who are a little more technical, [jitsi](https://jitsi.org/) offers an open-source video conferencing platform that you can install in your own server.  The whole project is available on [GitHub](https://github.com/jitsi).  If you feel like rolling your own solution, this is the way to go.

## Resources

- [WebRTC](https://webrtc.org/)
- [WebRTC Security Architecture](https://tools.ietf.org/html/draft-ietf-rtcweb-security-arch-20)