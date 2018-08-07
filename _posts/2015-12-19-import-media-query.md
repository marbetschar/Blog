---
id: 403
title: "@import media query"
date: 2015-12-19T18:30:07+00:00
author: Marco Betschart
description: CSS Code in Dateien auslagern und anhand von media queries anwenden.
layout: post
guid: http://marco.betschart.name/?p=403
permalink: /import-media-query/
thumb_image: /wp-content/uploads/2015/12/code-1084923-256x256.png
tags:
  - CSS
---
CSS Code in Dateien auslagern und anhand von media queries anwenden. Übersichtliches Responsive Design!

@import url('css/global.css');

/* Small Portrait */
@import url('css/small-portrait.css') only screen and (max-width: 479px);

/* Small Landscape */
@import url('css/small-landscape.css') only screen and (min-width: 480px) and (max-width: 767px);

/* Medium Portrait */
@import url('css/medium-portrait.css') only screen and (min-width: 768px) and (max-width: 959px);

/* Normal */
@import url('css/normal.css') only screen and (min-width: 960px);

Details und Kompatibilität im [Mozilla Developer Network](https://developer.mozilla.org/de/docs/Web/CSS/@import)