---
id: 663
title: Codify country name
date: 2016-07-05T12:50:54+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=663
permalink: /codify-country-name/
image: /wp-content/uploads/2015/12/code-1084923-256x256.png
categories:
  - Technologie
---
<div class="snippetcpt-wrap" id="snippet-664" data-id="664" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=664&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=664" data-fullscreen="http://dev.marco-betschart.local/code-snippets/codify-country-name/?full-screen=1">
  <pre class="prettyprint linenums lang-java" title="Codify country name">import java.util.Locale;

/**
Codifies country names to their ISO country code and vice versa:
    - LocaleCountry.nameOf("CH", new Locale("en")) -&gt; "Switzerland"
    - LocaleCountry.codeOf("Schweiz", new Locale("de")) -&gt; "CH"
    - LocaleCountry.codeExists("CH") -&gt; true
*/
public class LocaleCountry {
    
    public static String nameOf( String code ){
        return LocaleCountry.nameOf( code, Locale.getDefault() );
    }


    public static String nameOf( String code, Locale locale ){
        return new Locale(locale.getLanguage(),code.toUpperCase()).getDisplayCountry(locale);
    }
    
    
    public static String codeOf( String name ){
        Locale sys = Locale.getDefault();
        String code = LocaleCountry.codeOf(name, sys);
        
        if( code != null ){
            return code;
            
        } else if( !sys.getLanguage().equals("en") ){
            return LocaleCountry.codeOf(name,new Locale("en"));
        }
        
        return null;
    }
    
    
    public static String codeOf( String name, Locale locale ){
        String[] codes = Locale.getISOCountries();
        
        for( String code: codes ){
            if( name.equalsIgnoreCase(LocaleCountry.nameOf(code, locale)) ){
                return code;
            }
        }
        
        return null;
    }
    
    
    public static String codeOf( String name, Locale[] locales ){
        for( Locale locale: locales ){
            String code = LocaleCountry.codeOf(name, locale);
            
            if( code != null ){
                return code;
            }
        }
        
        return null;
    }
    
    
    public static boolean codeExists( String code ){
        String[] codes = Locale.getISOCountries();
        
        for( String comparison: codes ){
            if( code.equalsIgnoreCase(comparison) ){
                return true;
            }
        }
        
        return false;
    }
}</pre>
</div>