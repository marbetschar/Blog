---
id: 284
title: Code Snippets Shortcode
date: 2015-12-17T15:47:57+00:00
author: Marco Betschart
description: Ein Shortcode für das fantastische Code Snippets Plugin um Snippets aus diesem Plugin auch im Frontend darzustellen.
layout: post
guid: http://marco.betschart.name/?p=284
permalink: /code-snippets-shortcode/
thumb_image: uploads/2015/12/code-1084923-256x256.png
tags:
  - PHP
  - WordPress
---
**UPDATE:** [Fixed in Version 2.6.0](https://de.wordpress.org/plugins/code-snippets/changelog/)

<del datetime="2016-01-04T12:00:21+00:00">Ein Shortcode für das fantastische <a href="https://de.wordpress.org/plugins/code-snippets/" target="_blank">Code Snippets Plugin</a> um Snippets aus diesem Plugin auch im Frontend darzustellen:</del>

<div class="snippetcpt-wrap" id="snippet-524" data-id="524" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=524&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=524" data-fullscreen="http://dev.marco-betschart.local/code-snippets/code-snippet-shortcode/?full-screen=1">
  <pre class="prettyprint linenums lang-php" title="Code Snippet Shortcode">add_shortcode('snippet', function( $atts ){
  if( isset($atts['id']) ){
    $snippet = get_snippet( $atts['id'] );
  
      if( isset($snippet) ){
        if( class_exists('CrayonWP') ){
          return CrayonWP::highlight('&lt;pre&gt;'.htmlentities($snippet-&gt;code).'&lt;/pre&gt;');
          
        } else {
            return '&lt;pre&gt;'.htmlentities($snippet-&gt;code).'&lt;/pre&gt;';
        }
      }
  }
  
  return '';
});</pre>
</div>

<del datetime="2016-01-04T12:04:35+00:00">Und der <a href="https://github.com/sheabunge/code-snippets/issues/41" target="_blank">Feature Request</a>, dieses Feature direkt in das Plugin zu integrieren.</del>