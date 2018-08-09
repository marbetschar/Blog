---
id: 602
title: WordPress jQuery Version Downgrade
date: 2016-05-15T07:45:36+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=602
permalink: /wordpress-jquery-version-downgrade/
geo_latitude:
  - "48.139131"
geo_longitude:
  - "11.5801882"
geo_public:
  - "1"
geo_address:
  - München, Germany
thumb_image: uploads/2015/12/wordpress-589121.jpg
tags:
  - WordPress
---
<div class="snippetcpt-wrap" id="snippet-598" data-id="598" data-edit="/wp-admin/post.php?post=598&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=598" data-fullscreen="/code-snippets/downgrade-jquery/?full-screen=1">
  <pre class="prettyprint linenums lang-php" title="Downgrade jQuery">add_action('init', function(){
    if (!is_admin()) {
        wp_deregister_script('jquery');
        wp_register_script('jquery',
'//ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js', false, '1.8.3');
        wp_enqueue_script('jquery');
    }
});</pre>
</div>

<div id="geo-post-602" class="geo geo-post" style="display: none">
  <span class="latitude">48.139131</span><span class="longitude">11.5801882</span>
</div>