---
id: 596
title: Public Email Domain
date: 2016-05-07T19:51:29+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=596
permalink: /public-email-domain/
thumb_image: uploads/2015/12/code-1084923-256x256.png
tags:
  - Technologie
---
Check if a email string is an email address of a public email provider by just using this one liner in Swift:

<pre style="text-align: justify;">"marbetschar@gmail.com" ~= PublicEmailDomain.Any</pre>

<p style="text-align: justify;">
  Full Swift source code:
</p>

<p style="text-align: justify;">
  <div class="snippetcpt-wrap" id="snippet-595" data-id="595" data-edit="/wp-admin/post.php?post=595&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=595" data-fullscreen="/code-snippets/public-email-domain/?full-screen=1">
    <pre class="prettyprint linenums lang-swift" title="Public Email Domain">enum PublicEmailDomain: String{
    case Any
    case Aol = "^aol\\.[a-z]{2,5}$"
    case iCloud = "^icloud\\.com$"
    case Mac = "^mac\\.com$"
    case Me = "^me\\.com$"
    case Bluewin = "^bluewin\\.ch$"
    case Eclipso = "^eclipso\\.[a-z]{2,5}$"
    case Freenet = "^freenet\\.ch$"
    case Gmx = "^gmx\\.[a-z]{2,5}$"
    case Gmail = "^gmail\\.[a-z]{2,5}$"
    case Googlemail = "^googlemail\\.[a-z]{2,5}$"
    case Hotmail = "^hotmail\\.[a-z]{2,5}$"
    case Inbox = "^inbox\\.[a-z]{2,5}$"
    case Outlook = "^outlook\\.com$"
    case Live = "^live\\.[a-z]{2,5}$"
    case Msn = "^msn\\.com$"
    case Net24 = "^net-24\\.at$"
    case Online = "^online\\.de$"
    case TOnline = "^t-online\\.de$"
    case Web = "^web\\.[a-z]{2,5}$"
    case Yahoo = "^yahoo\\.[a-z]{2,5}$"
    case Zoho = "^zoho\\.[a-z]{2,5}$"
    case Yandex = "^yandex\\.[a-z]{2,5}$"
    
    static let allValues: [PublicEmailDomain] = [
        Aol,
        iCloud,
        Mac,
        Me,
        Bluewin,
        Eclipso,
        Freenet,
        Gmx,
        Gmail,
        Googlemail,
        Hotmail,
        Inbox,
        Outlook,
        Live,
        Msn,
        Net24,
        Online,
        TOnline,
        Web,
        Yahoo,
        Zoho,
        Yandex
    ]
}

extension PublicEmailDomain: Equatable{}

func == (lhs: String, rhs: PublicEmailDomain) -&gt; Bool{
    
    switch(rhs){
    case .Any:
        for publicEmailDomain in PublicEmailDomain.allValues{
            if lhs == publicEmailDomain {
                return true
            }
        }
        return false
        
    default:
        do{
            return try NSRegularExpression(pattern: rhs.rawValue, options: .CaseInsensitive).numberOfMatchesInString(lhs, options: [], range: NSMakeRange(0, lhs.characters.count)) == 1
            
        } catch _{
            return false
        }
    }
}


func ~=(email: String, publicEmailDomain: PublicEmailDomain) -&gt; Bool{
    let domain: String = {
        let parts = email.characters.split{$0 == "@"}.map(String.init)
        return parts[parts.count - 1]
    }()

    return domain == publicEmailDomain
}</pre>
  </div>
</p>

&nbsp;