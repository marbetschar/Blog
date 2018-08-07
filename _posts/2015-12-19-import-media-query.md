---
id: 403
title: @import media query
date: 2015-12-19T18:30:07+00:00
author: Marco Betschart
excerpt: CSS Code in Dateien auslagern und anhand von media queries anwenden.
layout: post
guid: http://marco.betschart.name/?p=403
permalink: /import-media-query/
image: /wp-content/uploads/2015/12/code-1084923-256x256.png
tags:
  - CSS
---
CSS Code in Dateien auslagern und anhand von media queries anwenden. Übersichtliches Responsive Design!

<div class="snippetcpt-wrap" id="snippet-500" data-id="500" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=500&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=500" data-fullscreen="http://dev.marco-betschart.local/code-snippets/import-media-queries/?full-screen=1">
  <pre class="prettyprint linenums lang-css" title="@import media queries">@import url('css/global.css');

/* Small Portrait */
@import url('css/small-portrait.css') only screen and (max-width: 479px);

/* Small Landscape */
@import url('css/small-landscape.css') only screen and (min-width: 480px) and (max-width: 767px);

/* Medium Portrait */
@import url('css/medium-portrait.css') only screen and (min-width: 768px) and (max-width: 959px);

/* Normal */
@import url('css/normal.css') only screen and (min-width: 960px);</pre>
</div>

Details und Kompatibilität im [Mozilla Developer Network](https://developer.mozilla.org/de/docs/Web/CSS/@import)