---
title: 'FolderBar: A new approach to more than 5 Tabs in a UITabBar'
date: 2016-07-20T19:30:59+00:00
author: Marco Betschart
layout: post
permalink: /folderbar-a-new-approach-for-more-than-5-tabs-in-the-uitabbar/
thumb_image: uploads/2016/07/FolderBar-More-Items-Active.png
tags:
  - Apps
  - Empfehlungen
  - Technologie
---
You may already came across the Apple tab limitation for the UITabBarController: You are only allowed to have a maximum of 5 tabs in a UITabBar.

|:------------- | -------------:|
| ![UITabBar More Items]({% asset 'uploads/2016/07/UITabBar-More-Items.png' @path %}) | ![UITabBar More Items Active]({% asset 'uploads/2016/07/UITabBar-More-Items-Active.png' @path %}) |

If you got more than these five items, an inconvenient and ugly moreNavigationController takes over and ruins your whole ui experience by it&#8217;s unnatural and complex user interface.

Well, you may argue if you got that much tabs you should rethink the navigation structure of your app &#8211; or the app as a whole. A lot of times this is true, but there are also a few total valid use cases.

In those valid cases, you had to circumvent the &#8222;More-Problem&#8220; by using the well-known hamburger menu. This approach is far from ideal and there is a huge discussion going on. Simply have a brief look around and you&#8217;ll find a lot of resources (for example [this one](https://lmjabreu.com/post/why-and-how-to-avoid-hamburger-menus/)).

Long story short: I&#8217;ve decided to went down a new path.

|:------------- | -------------:|
| ![FolderBar More Items]({% asset 'uploads/2016/07/FolderBar-More-Items.png' @path %}) | ![FolderBar More Items Active]({% asset 'uploads/2016/07/FolderBar-More-Items-Active.png' @path %}) |

The idea is simple:

We just want the UITabBar to behave like any iOS Folder. That was the birth of the all new and shiny _FolderBar_.

  1. The _FolderBar_ can be opened if there are more than 5 items by tapping the open handle which is automagically added &#8211; or you can simply use a swipe gesture
  2. All items can be rearranged with drag & drop
  3. 1&2 together provide a simple, self explanatory and fully customizable quick access for the user &#8211; because the four upper items are never hidden

If you&#8217;re interested in integrating _FolderBar_ in your project, simply drop me a line: <folderbar@marco.betschart.name>