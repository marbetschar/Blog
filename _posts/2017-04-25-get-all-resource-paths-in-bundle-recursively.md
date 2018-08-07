---
id: 720
title: Get all resource paths in bundle recursively
date: 2017-04-25T20:10:52+00:00
author: Marco Betschart
excerpt: "I've been looking for a way to search a subdirectory in my main bundle recursively - the following simple Swift extension does the trick."
layout: post
guid: https://marco.betschart.name/?p=720
permalink: /get-all-resource-paths-in-bundle-recursively/
image: /wp-content/uploads/2015/12/code-1084923-256x256.png
tags:
  - Swift
---
I&#8217;ve been looking for a way to search a subdirectory in my main bundle recursively &#8211; the following simple Swift extension does the trick.

#### `Bundle.main.paths(forResource: String?, ofType: String?) -> [String]?`

`<br />
let paths: [String]? = Bundle.main.paths(forResource: "my-resource", ofType: "my-extension")`

#### `Bundle.main.urls(forResource: String?, withExtension: String?) -> [URL]?`

`let urls: [URL]? = Bundle.main.urls(forResource: "my-resource", withExtension: "my-extension")<br />
` 

#### The source code of the extension

<div class="snippetcpt-wrap" id="snippet-719" data-id="719" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=719&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=719" data-fullscreen="http://dev.marco-betschart.local/code-snippets/get-all-resource-paths-in-bundle-recursively/?full-screen=1">
  <pre class="prettyprint linenums lang-swift" title="Get all resource paths in bundle recursively">import Foundation

extension Bundle{
    
    func urls(forResource name: String?, withExtension ext: String?) -&gt; [URL]?{
        guard let resourceURL = self.resourceURL else{ return nil }
        let enumerator = FileManager.default.enumerator(at: resourceURL, includingPropertiesForKeys: nil)
        
        var urls = [URL]()
        while let url = enumerator?.nextObject() as? URL{
            guard ext == nil && url.lastPathComponent == name || ext == url.pathExtension && url.deletingPathExtension().lastPathComponent == name else{
                continue
            }
            urls.append(url)
        }
        
        return urls.count &gt; 0 ? urls : nil
    }
    
    func paths(forResource name: String?, ofType type: String?) -&gt; [String]?{
        return self.urls(forResource: name, withExtension: type)?.map{ $0.path }
    }
}</pre>
</div>