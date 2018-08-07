---
title: Get all resource paths in bundle recursively
date: 2017-04-25T20:10:52+00:00
description: "I've been looking for a way to search a subdirectory in my main bundle recursively - the following simple Swift extension does the trick."
layout: post
permalink: /get-all-resource-paths-in-bundle-recursively/
thumb_image: uploads/2015/12/code-1084923-256x256.png
tags:
  - Swift
---

#### `Bundle.main.paths(forResource: String?, ofType: String?) -> [String]?`

    {% highlight swift %}
    let paths: [String]? = Bundle.main.paths(forResource: "my-resource", ofType: "my-extension")
    {% endhighlight %}

#### `Bundle.main.urls(forResource: String?, withExtension: String?) -> [URL]?`

    {% highlight swift %}
    let urls: [URL]? = Bundle.main.urls(forResource: "my-resource", withExtension: "my-extension")
    {% endhighlight %}

#### The source code of the extension

    {% highlight swift %}
    import Foundation

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
    }
    {% endhighlight %}
