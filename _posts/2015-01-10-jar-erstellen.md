---
title: JAR erstellen
date: 2015-01-10T01:42:23+00:00
description: Eine kurze Anleitung, wie eine JAR (Java ARchive) Datei aus Java Source Code generiert wird.
layout: post
permalink: /jar-erstellen/
thumb_image: uploads/2015/12/code-1084923-256x256.png
tags:
  - Java
---
Wir verwenden folgenden Code um ein Beispielprogramm zu erzeugen, das „Hello World!“ auf der Kommandozeile ausgibt:

    {% highlight bash %}
    $: vi HelloWorld.java
    {% endhighlight %}

    {% highlight java %}
    /**
    * The HelloWorld class implements an application that
    * simply prints "Hello World!" to standard output.
    */
    class HelloWorld {
      public static void main(String[] args) {
        System.out.println("Hello World!"); // Display the string.
      }
    }
    {% endhighlight %}

Um nun daraus eine lauffähige `*.jar` Datei zu machen, muss als erstes ein `MANIFEST` erstellt werden. Dieses beinhaltet den Namen der Hauptklasse, die als Einstiegspunkt des Programms verwendet werden soll. Der Name der `MANIFEST` Datei spielt dabei keine Rolle, Java passt ihren Namen automatisch bei der Erstellung der JAR Archivs an.

    {% highlight bash %}
    $: vi manifest.txt
    Main-Class: HelloWorld
    {% endhighlight %}

Im nächsten Schritt kompilieren wir den Quellcode der `HelloWorld.java` Datei in ausführbaren Bytecode:

    {% highlight bash %}
    $: javac HelloWorld.java
    {% endhighlight %}

Und als letztes packen wir alles zusammen in ein `helloworld.jar `Archiv. Weitere Dateien können durch ein Leerzeichen getrennt hinzugefügt werden. Sollte es sich um ein Verzeichnis handeln, so wird dieses rekursiv hinzugefügt:

    {% highlight bash %}
    $: jar -cvfm helloworld.jar manifest.txt HelloWorld.class
    {% endhighlight %}

Et voilà, schon haben wir unser ausführbares „Hello World!“ Java Programm:

    {% highlight bash %}
    $: java -jar helloworld.jar
    Hello World!
    {% endhighlight %}
