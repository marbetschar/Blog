---
id: 379
title: Tomcat Heap Space
date: 2015-08-10T17:49:46+00:00
author: Marco Betschart
layout: post
guid: http://marco.betschart.name/?p=379
permalink: /tomcat-heap-space/
image: /wp-content/uploads/2015/12/code-1084923-256x256.png
tags:
  - Java
  - Tomcat
---
<div class="snippetcpt-wrap" id="snippet-495" data-id="495" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=495&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=495" data-fullscreen="http://dev.marco-betschart.local/code-snippets/tomcat-heap-space/?full-screen=1">
  <pre class="prettyprint linenums lang-bash" title="Tomcat Heap Space">$~: sudo vi tomcat/bin/setenv.sh
JAVA_OPTS="-Xms256m -Xmx1024m"</pre>
</div>

  * `Xms` specifies the initial memory allocation pool for a Java Virtual Machine.
  * `Xmx` specifies the maximum memory allocation pool.

This means that your JVM will be started with `Xms` amount of memory and will be able to use a maximum of `Xmx` amount of memory.