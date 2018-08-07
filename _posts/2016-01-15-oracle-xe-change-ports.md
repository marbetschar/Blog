---
id: 414
title: 'Oracle XE: Change Ports'
date: 2016-01-15T08:46:50+00:00
author: Marco Betschart
layout: post
guid: http://marco.betschart.name/?p=414
permalink: /oracle-xe-change-ports/
thumb_image: /wp-content/uploads/2016/01/server-90389_1920-256x256.jpg
tags:
  - Oracle
  - SQL
---
Um die Standartports von Oracle XE zu ändern, einfach folgende Schritte ausführen:

  1. Verbindung zu Oracle XE mit SQLPlus aufbauen
  
    <div class="snippetcpt-wrap" id="snippet-517" data-id="517" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=517&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=517" data-fullscreen="http://dev.marco-betschart.local/code-snippets/sqlplus-connect/?full-screen=1">
      <pre class="prettyprint linenums lang-bash" title="SQLPlus Connect">$: sqlplus system
SQL*Plus: Release 11.2.0.2.0 Production on Mo Dez 21 18:59:09 2015
Copyright (c) 1982, 2014, Oracle.  All rights reserved.

Enter password:

Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL&gt;</pre>
    </div>

  2. Aktuelle Ports anzeigen
  
    <div class="snippetcpt-wrap" id="snippet-518" data-id="518" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=518&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=518" data-fullscreen="http://dev.marco-betschart.local/code-snippets/sqlplus-http-ftp-port/?full-screen=1">
      <pre class="prettyprint linenums lang-bash" title="SQLPlus HTTP & FTP Port">SQL&gt; SELECT DBMS_XDB.getHttpPort AS "HTTP-Port"
,DBMS_XDB.getFtpPort AS "FTP-Port" FROM dual;

HTTP-Port FTP-Port
--------- ----------
     8080          0</pre>
    </div>

  3. Ports anpassen
  
    <div class="snippetcpt-wrap" id="snippet-519" data-id="519" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=519&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=519" data-fullscreen="http://dev.marco-betschart.local/code-snippets/sqlplus-http-ftp-port-anpassen/?full-screen=1">
      <pre class="prettyprint linenums lang-bash" title="SQLPlus HTTP & FTP Port anpassen">SQL&gt; BEGIN
  DBMS_XDB.setHttpPort('3030');
  DBMS_XDB.setFtpPort('2100');
END;
/

PL/SQL procedure successfully completed.</pre>
    </div>

  4. Extra: Dienst Deaktivieren
  
    Wenn der Port auf `` gesetzt wird, deaktiviert das den Dienst.