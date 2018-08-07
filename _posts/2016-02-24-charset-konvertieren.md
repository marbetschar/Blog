---
id: 553
title: Charset Konvertieren
date: 2016-02-24T19:07:00+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=553
permalink: /charset-konvertieren/
image: /wp-content/uploads/2015/12/code-1084923-256x256.png
categories:
  - Technologie
tags:
  - Charset
  - Java
  - Oracle
  - SQL
---
Java unterstützt auf einfache Art und Weise die Konvertierung von Zeichensätzen:

<div class="snippetcpt-wrap" id="snippet-564" data-id="564" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=564&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=564" data-fullscreen="http://dev.marco-betschart.local/code-snippets/charset-convert/?full-screen=1">
  <pre class="prettyprint linenums lang-java" title="Charset Convert">import java.nio.ByteBuffer;
import java.nio.charset.Charset;

Charset utf8 = Charset.forName("UTF-8");
Charset iso88591 = Charset.forName("ISO-8859-1");

//get byte array from string
ByteBuffer utf8Buffer = ByteBuffer.wrap( utf8String.getBytes() );

//convert byte array from UTF-8 to ISO-8859-1
ByteBuffer iso88591Buffer = iso88591.encode( utf8.decode( utf8Buffer ) );

//parse byte array to ISO-8859-1 string
String iso88591String = new String( iso88591Buffer.array(), "ISO-8859-1" ); </pre>
</div>

Nähere Angaben zu den unterstützten Zeichensätzen findet sich in der <a href="https://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html" target="_blank">Dokumentation der Klasse Charset</a>.

Um mit Java die Daten aus einer Oracle Datenbank von ISO-8859-1 in UTF-8 konvertieren kann man folgendermassen vorgehen:

<div class="snippetcpt-wrap" id="snippet-552" data-id="552" data-edit="http://dev.marco-betschart.local/wp-admin/post.php?post=552&action=edit" data-copy="/wp-admin/export.php?type=jekyll&#038;snippet=b31d996337&#038;id=552" data-fullscreen="http://dev.marco-betschart.local/code-snippets/oracle-charset-convert/?full-screen=1">
  <pre class="prettyprint linenums lang-java" title="Oracle Charset Convert">import java.io.UnsupportedEncodingException;
import java.nio.ByteBuffer;
import java.nio.charset.Charset;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

Class.forName("oracle.jdbc.driver.OracleDriver");
Connection connection = DriverManager.getConnection("jdbc:oracle:thin:@server:port:sid", "username", "password");

PreparedStatement selectStmt = connection.prepareStatement("SELECT id,subject FROM messages");
ResultSet resultSet = selectStmt.executeQuery();

Charset utf8 = Charset.forName("UTF-8");
Charset iso88591 = Charset.forName("ISO-8859-1");

System.out.println( "Converting Records..." );

while( resultSet.next() ){
    byte[] raw = resultSet.getBytes("subject");
    ByteBuffer iso88591Buffer = ByteBuffer.wrap(raw);

    //do the actual charset conversion
    ByteBuffer utf8Buffer = utf8.encode( iso88591.decode(iso88591Buffer) );
    
    try{
        String iso88591Str = new String(iso88591Buffer.array(),"UTF8");
        String utf8Str = new String(utf8Buffer.array(),"UTF8");
        
        System.out.println("UTF8: '" + iso88591Str + "' =&gt; '" + utf8Str + "'");
        
        PreparedStatement updateStmt = connection.prepareStatement("UPDATE messages SET subject = ? WHERE id = ?");
        updateStmt.setString(1,utf8Str);
        updateStmt.setInt(2, resultSet.getInt("id"));
        updateStmt.executeUpdate();
        updateStmt.close();
        
    } catch( UnsupportedEncodingException e ){}
}

if( selectStmt != null ){
    selectStmt.close();
}</pre>
</div>