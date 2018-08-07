---
title: JAR vs. WAR vs. EAR
layout: post
date: 2015-01-02T01:38:07+00:00
description: Die Unterschiede der Java Archive JAR, WAR und EAR kurz und knackig zusammengefasst.
permalink: /jar-war-ear/
thumb_image: uploads/2015/12/code-1084923-256x256.png
tags:
  - Java
---
## JAR

Java Archive beinhalten `*.class` Dateien, Bibliotheken, statische Dateien und ein optionales `META-INF/MANIFEST.MF`. Dieses optionale `MANIFEST.MF` kann Versionsinformationen und andere Beschreibungen der Archivs beinhalten.

## WAR

Web Archive beinhalten eine vollständige Java Web Applikation, die auf einem Servlet Container wie zBsp. Apache Tomcat deployed werden kann. Das Archiv enthält alle dazu notwendigen statischen als auch `\*.jsp`, `\*.css`, `\*.js` oder `\*.jar` Dateien. Zusätzlich dazu besitzt das Web Archiv ein `WEB-INF/web.xml` Deployment Descriptor, der dem Servlet Container mitteilt, wie das Archiv korrekt deployed wird.

## EAR

Enterprise Archive können mehrere `\*.war` und `\*.jar` Dateien beinhalten und vereinfachen so das Deployment komplexer Enterprise Applikationen.