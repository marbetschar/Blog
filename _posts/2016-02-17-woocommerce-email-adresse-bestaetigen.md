---
id: 541
title: 'WooCommerce: E-Mail Adresse bestätigen'
date: 2016-02-17T12:29:30+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=541
permalink: /woocommerce-email-adresse-bestaetigen/
thumb_image: uploads/2015/12/wordpress-589121-256x256.jpg
tags:
  - PHP
  - WooCommerce
  - WordPress
---
Im WooCommerce Checkout Prozess lässt sich ganz einfach ein zusätzliches Feld für die Validierung der eingegebenen E-Mail-Adresse hinzufügen:

<a href="/assets/uploads/2016/02/billing_email_confirm.png" rel="attachment wp-att-546"><img class="alignnone size-full wp-image-546" src="/assets/uploads/2016/02/billing_email_confirm.png" alt="billing_email_confirm" width="812" height="164" srcset="/assets/uploads/2016/02/billing_email_confirm.png 812w, uploads/2016/02/billing_email_confirm-300x61.png 300w, uploads/2016/02/billing_email_confirm-768x155.png 768w, uploads/2016/02/billing_email_confirm-192x39.png 192w" sizes="(max-width: 812px) 100vw, 812px" /></a>

<div class="snippetcpt-wrap" id="snippet-540" data-id="540" data-edit="/wp-admin/post.php?post=540&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=540" data-fullscreen="/code-snippets/checkout-email-confirm/?full-screen=1">
  <pre class="prettyprint linenums lang-php" title="Checkout E-Mail Confirm">add_filter('woocommerce_checkout_fields',function($fields){
    $billing_email_confirm = array(
        'label'            =&gt; 'E-Mail-Adresse best&auml;tigen',
        'placeholder'    =&gt; '',
        'required'        =&gt; true,
        'class'            =&gt; apply_filters('woocommerce_billing_email_confirm_field_class',array('form-row-first')),
        'clear'            =&gt; true,
        'validate'        =&gt; array('email'),
    );
    $billing_email_index = array_search('billing_email', array_keys($fields['billing']));
  
    if( $billing_email_index ){
        $fields['billing'] = array_slice($fields['billing'],0,$billing_email_index + 1,true) +
            array( 'billing_email_confirm' =&gt; $billing_email_confirm ) +
            array_slice($fields['billing'],$billing_email_index + 1,null,true);
    } else {
        $fields['billing']['billing_email_confirm'] = $billing_email_confirm;
    }

    return $fields;
});

add_filter('woocommerce_process_checkout_field_billing_email_confirm',function($email_confirm=''){
    global $woocommerce;
    $billing_email = $woocommerce-&gt;checkout-&gt;posted['billing_email'];

    if( strtolower($email_confirm) != strtolower($billing_email) ){
        $notice = '&lt;strong&gt;E-Mail-Adressen stimmen nicht &uuml;berein&lt;/strong&gt;';

        if ( version_compare( WC_VERSION, '2.3', '&lt;' ) ) {
            $woocommerce-&gt;add_error($notice);
        } else {
            wc_add_notice($notice,'error');
        }
    }

    return $email_confirm;
});

add_filter('default_checkout_billing_email_confirm',function($value=null,$field='billing_email_confirm'){
    if( is_user_logged_in() ){
        global $current_user;
        $value = $current_user-&gt;user_email;
    }
    return $value;
},10,2);</pre>
</div>