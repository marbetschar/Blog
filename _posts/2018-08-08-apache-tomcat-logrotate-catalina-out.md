---
title: Apache Tomcat Logrotate catalina.out
layout: post
date: 2018-08-08 12:02:22 +0200
thumb_image: uploads/2018/08/apache-tomcat-logrotate-catalina-out.jpg
description: Howto rotate the Apache Tomcat log file and avoid ending up with a huge
  catalina.out
permalink: "/apache-tomcat-logrotate-catalina-out/"
tags:
- Apache Tomcat
- Java
- Logrotate
- Linux

---
{% include image.html path="uploads/2018/08/apache-tomcat-logrotate-catalina-out.jpg" path-detail="uploads/2018/08/apache-tomcat-logrotate-catalina-out.jpg" alt="Apache Tomcat Logrotate catalina.out" %}

Apache Tomcat logs everything into `catalina.out`: `System.out`, `System.err` as well as regular logs used by logging facilities such as `log4j`.

Additionally the Tomcat also logs into `catalina.YYYY-MM-dd.log` files. In contrast to the catalina.out those files do only contain logs from logging facilities - but not from `System.out` or `System.err`.

### Disable `catalina.YYYY-MM-dd.log`

Developers should not use `System.out` and `System.err` in production - but in reality this is not always the case. To ensure we do not miss any logs we first avoid doubling the log information by deactivating `catalina.YYYY-MM-dd.log` in `conf/logging.properties`; Just comment the following lines an restart Apache Tomcat:

    {% highlight bash %}
    # 1catalina.org.apache.juli.AsyncFileHandler.level = INFO
    # 1catalina.org.apache.juli.AsyncFileHandler.directory = ${catalina.base}/logs
    # 1catalina.org.apache.juli.AsyncFileHandler.prefix = catalina.
    {% endhighlight %}

### Rotate `catalina.out`

Every output is logged to `catalina.out`. So it can grow fairly big. To avoid ending up with a huge file, we simply rotate it by using the Linux `logrotate` tool. For this, add the following configuration in `/etc/logrotate.d/apache-tomcat`:

    {% highlight bash %}
    /opt/apache-tomcat/logs/catalina.out {
      # Daily rotation
        daily
      # We keep original file live
        copytruncate
      # If file is missing keep working
        missingok
      # limit the number of log file rotation. This keeps only the recent 30 log files
        rotate 30
      # Add the date in the file name
        dateext
      # Set the format of the date which should be added
        dateformat .%Y-%m-%d
      # Set the filename extension which should be used
        extension .out
    }
    {% endhighlight %}

Last but not least, make sure `logrotate` is executed daily via `cron` by verifying the existence of the following file:

    {% highlight bash %}
    $: ls /etc/cron.daily/logrotate
    {% endhighlight %}

#### References

* Photo by [Radek Grzybowski](https://unsplash.com/photos/8tem2WpFPhM?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/wood-logs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)