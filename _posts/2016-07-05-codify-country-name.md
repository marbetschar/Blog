---
title: Codify country name
date: 2016-07-05 12:50:54 +0000
description: Java Snippet to codify country names to their ISO country code and vice versa.
author: Marco Betschart
layout: post
permalink: "/codify-country-name/"
image: "/wp-content/uploads/2015/12/code-1084923-256x256.png"
categories:
- Java
---

    {% highlight java %}
    import java.util.Locale;
    /**
    Codifies country names to their ISO country code and vice versa:
    - LocaleCountry.nameOf("CH", new Locale("en")) -> "Switzerland"
    - LocaleCountry.codeOf("Schweiz", new Locale("de")) -> "CH"
    - LocaleCountry.codeExists("CH") -> true
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
    }
    {% endhighlight %}
