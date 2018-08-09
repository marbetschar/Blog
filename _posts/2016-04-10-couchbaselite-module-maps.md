---
id: 587
title: 'CouchbaseLite &#8211; Module maps'
date: 2016-04-10T15:56:22+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=587
permalink: /couchbaselite-module-maps/
thumb_image: uploads/2015/12/code-1084923-256x256.png
tags:
  - Technologie
---
As convenient as the bridging header is, it has one key limitation—you can’t use it inside a framework project.  The alternative is to use a [module](http://clang.llvm.org/docs/Modules.html "Clang Module documentation").

This can be problematic when using Couchbase Lite for iOS for example.

To do this, create a directory in your project directory named `CouchbaseLite`. Inside the directory, create a `module.map` file that encapsulates library settings. For `CouchbaseLite`, `module.map` looks like this:

<pre>module CouchbaseLite {
  header "../Pods/couchbase-lite-ios/CouchbaseLite.framework/Headers/CouchbaseLite.h"
  export *
}</pre>

Now add the new module to Import Paths under Swift Compiler – Search Paths in your project settings. Use ${SRCROOT} in the module path (e.g. ${SRCROOT}/CouchbaseLite) to insure that the project works no matter where it’s checked out.

<a href="/assets/uploads/2016/04/SwiftCompiler-Search-Paths-CouchbaseLite.png" rel="attachment wp-att-588"><img class="alignnone wp-image-588" src="/assets/uploads/2016/04/SwiftCompiler-Search-Paths-CouchbaseLite-300x41.png" alt="SwiftCompiler - Search Paths - CouchbaseLite" width="770" height="106" srcset="/assets/uploads/2016/04/SwiftCompiler-Search-Paths-CouchbaseLite-300x41.png 300w, uploads/2016/04/SwiftCompiler-Search-Paths-CouchbaseLite-768x106.png 768w, uploads/2016/04/SwiftCompiler-Search-Paths-CouchbaseLite-1024x141.png 1024w, uploads/2016/04/SwiftCompiler-Search-Paths-CouchbaseLite-192x26.png 192w, uploads/2016/04/SwiftCompiler-Search-Paths-CouchbaseLite.png 1118w" sizes="(max-width: 770px) 100vw, 770px" /></a>

This makes it possible to just `import CouchbaseLite` in your Swift files. Note that consumers of any frameworks you build using this technique are also going to have to add the module to their Swift search paths.

[Many thanks and © to Matt Behrens!](https://spin.atomicobject.com/2015/02/23/c-libraries-swift/)