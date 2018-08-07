---
id: 454
title: 'WordPress: Alle Rollen'
date: 2016-01-24T02:39:31+00:00
author: Marco Betschart
layout: post
guid: http://marco.betschart.name/?p=454
permalink: /wordpress-alle-rollen/
thumb_image: uploads/2015/12/wordpress-589121-256x256.jpg
tags:
  - PHP
  - WordPress
---
Um alle Benutzerrollen von WordPress auszulesen:

<div class="snippetcpt-wrap" id="snippet-502" data-id="502" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=502&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=502" data-fullscreen="http://dev.marco-betschart.local/code-snippets/all-user-roles/?full-screen=1">
  <pre class="prettyprint linenums lang-php" title="All user roles">$editable_roles = get_editable_roles();</pre>
</div>

Diese Abfrage liefert gleich auch alle Berechtigungen mit.