---
id: 729
title: 'Cloudron: Migrate app to different instance'
date: 2017-07-17T19:18:04+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=729
permalink: /cloudron-migrate-app-to-different-instance/
tags:
  - Cloudron
  - Linux
---
Migrating apps from one Cloudron to another works by first creating a new backup of the app on the old Cloudron, copying the backup tarball onto the new Clodron&#8217;s backup storage and then installing a new app, based on the backup on the new Cloudron.

#### Prerequisites

  * _Both Cloudrons have to use the same backup encryption key &#8211; or none at all 😉_
  * <a href="https://git.cloudron.io/cloudron/cloudron-cli/" target="_blank" rel="noopener"><em>Cloudron CLI installed on local machine</em></a>

### The following steps will migrate an app

**#1 Create a backup on the old Cloudron**

<pre>$: cloudron login
$: cloudron list
$: cloudron backup create --app &lt;appid&gt;
$: cloudron logout</pre>

**#2 Copy the new backup from the old Cloudron&#8217;s backup storage to the new one**

<pre>It depends on your backup solution where your newly created backup is stored.
Use the same path for the new Cloudron correspondingly.</pre>

**#3 Then login to the new Cloudron and install the new app based on the created backup**

<pre>$: cloudron login
$: cloudron install --appstore-id=org.wordpress.cloudronapp --backup .../...tar.gz
$: cloudron logout</pre>

<a href="https://git.cloudron.io/cloudron/box/commit/04d6f94108cbb9b17bb831912c0c47881a177d98" target="_blank" rel="noopener">© Cloudron.io</a>