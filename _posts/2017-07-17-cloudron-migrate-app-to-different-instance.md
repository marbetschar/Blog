---
id: 729
title: 'Cloudron: Migrate app to different instance'
date: 2017-07-17 19:18:04 +0000
author: Marco Betschart
layout: post
guid: ''
permalink: "/cloudron-migrate-app-to-different-instance/"
tags:
- Cloudron
- Linux

---
Migrating apps from one Cloudron to another works by first creating a new backup of the app on the old Cloudron, copying the backup tarball onto the new Clodron’s backup storage and then installing a new app, based on the backup on the new Cloudron.

#### Prerequisites

* Both Cloudrons have to use the same backup encryption key – or none at all 😉
* [Cloudron CLI installed on local machine](https://git.cloudron.io/cloudron/cloudron-cli/)

### The following steps will migrate an app

**#1 Create a backup on the old Cloudron**

    {% highlight bash %}
    $: cloudron login
    $: cloudron list
    $: cloudron backup create --app <appid>
    $: cloudron logout
    {% endhighlight %}

**#2 Copy the new backup from the old Cloudron’s backup storage to the new one**

It depends on your backup solution where your newly created backup is stored. Use the same path for the new Cloudron correspondingly.

**#3 Then login to the new Cloudron and install the new app based on the created backup**

    {% highlight bash %}
    $: cloudron login
    $: cloudron install --appstore-id=org.wordpress.cloudronapp --backup .../...tar.gz
    $: cloudron logout
    {% endhighlight %}

[© Cloudron.io](https://git.cloudron.io/cloudron/box/commit/04d6f94108cbb9b17bb831912c0c47881a177d98)