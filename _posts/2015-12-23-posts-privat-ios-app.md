---
id: 355
title: 'Posts &#8222;Privat&#8220; by Default &#8211; iOS App'
date: 2015-12-23T21:11:53+00:00
author: Marco Betschart
layout: post
guid: http://marco.betschart.name/?p=355
permalink: /posts-privat-ios-app/
image: /wp-content/uploads/2015/12/wordpress-589121-256x256.jpg
tags:
  - PHP
  - WordPress
---
Die Sichtbarkeit neuer Posts die aus der WordPress App erstellt werden automatisch auf _Privat_ setzen:

<div class="snippetcpt-wrap" id="snippet-486" data-id="486" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=486&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=486" data-fullscreen="http://dev.marco-betschart.local/code-snippets/private-posts-default-admin/?full-screen=1">
  <pre class="prettyprint linenums lang-php" title="Private Posts by Default - Admin">add_action('post_submitbox_misc_actions',function(){
  global $post;
  
  if( 'publish' == $post-&gt;post_status ){
    $visibility = 'public';
    $i18n = __('Public');
    
  } elseif( !empty( $post-&gt;post_password ) ){
    $visibility = 'password';
    $i18n = __('Password protected');
    
  } elseif ( $post_type == 'post' && is_sticky( $post-&gt;ID ) ) {
    $visibility = 'public';
    $i18n = __('Public, Sticky');

  } else {
    $post-&gt;post_password = '';
    $visibility = 'private';
    $i18n = __('Private');
  }
  
  echo '&lt;script type="text/javascript"&gt;(function($){'.
    'try{'.
      '$("#post-visibility-display").text("'.$i18n.'");'.
      '$("#hidden-post-visibility").val("'.$visibility.'");'.
      '$("#visibility-radio-'.$visibility.'").prop("checked", true);'.
    '} catch(err){}'.
  '})(jQuery);&lt;/script&gt;';
});</pre>
</div>