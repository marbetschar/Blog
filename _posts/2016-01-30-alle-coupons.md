---
id: 457
title: 'WooCommerce: Alle coupons'
date: 2016-01-30T05:09:32+00:00
author: Marco Betschart
layout: post
guid: http://marco.betschart.name/?p=457
permalink: /alle-coupons/
thumb_image: uploads/2015/12/wordpress-589121.jpg
tags:
  - PHP
  - WooCommerce
---
Um alle Coupons aus WooCommerce auszulesen:

<div class="snippetcpt-wrap" id="snippet-503" data-id="503" data-edit="/wp-admin/post.php?post=503&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=503" data-fullscreen="/code-snippets/all-coupons/?full-screen=1">
  <pre class="prettyprint linenums lang-php" title="All coupons">$args = array(
  'posts_per_page'    =&gt; -1,
  'orderby'            =&gt; 'title',
  'order'            =&gt; 'asc',
  'post_type'        =&gt; 'shop_coupon',
  'post_status'        =&gt; 'publish'
);
$coupons = get_posts( $args );</pre>
</div>