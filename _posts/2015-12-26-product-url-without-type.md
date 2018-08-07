---
id: 391
title: Product URL without Type
date: 2015-12-26T14:52:50+00:00
author: Marco Betschart
excerpt: Produkte in WooCommerce aufrufen, ohne den /product Slug in der URL.
layout: post
guid: http://marco.betschart.name/?p=391
permalink: /product-url-without-type/
image: /wp-content/uploads/2015/12/wordpress-589121-256x256.jpg
tags:
  - PHP
  - WooCommerce
  - WordPress
---
Um Produkte in WooCommerce direkt aufzurufen, ohne den `/product` Slug in der URL zu haben, kann folgender Schnipsel verwendet werden:

<div class="snippetcpt-wrap" id="snippet-497" data-id="497" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=497&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=497" data-fullscreen="http://dev.marco-betschart.local/code-snippets/product-url-wo-type-slug/?full-screen=1">
  <pre class="prettyprint linenums lang-php" title="Post URL w/o Type Slug">add_filter('post_type_link',function($permalink, $post, $leavename){
    if (!gettype($post) == 'post') {
        return $permalink;
    }
  
    switch ($post-&gt;post_type) {
        case 'product':
            if( !strpos($permalink,'?') ){
                $permalink = get_home_url() . '/' . $post-&gt;post_name . '/';
            }
            break;
    }
 
    return $permalink;
},10,3);

add_action('pre_get_posts',function( $query ){
    global $wpdb;
 
    if(!$query-&gt;is_main_query()) {
        return;
    }
    $post_name = $query-&gt;get('pagename');

    $post_type = $wpdb-&gt;get_var(
        $wpdb-&gt;prepare(
            'SELECT post_type FROM ' . $wpdb-&gt;posts . ' WHERE post_name = %s AND post_type != \'attachment\' LIMIT 1',
            $post_name
        )
    );
 
    switch($post_type) {
        case 'product':
            $query-&gt;set('product', $post_name);
            $query-&gt;set('post_type', $post_type);
            $query-&gt;is_single = true;
            $query-&gt;is_page = false;
            break;
    }
});</pre>
</div>