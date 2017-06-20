---
layout: post
title: Including UML Graphs in Javadoc
categories: programming
tags: java javadoc
---
## Install
```
$ brew install graphviz
$ which dot
```

## Configure
```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-javadoc-plugin</artifactId>
  <configuration>
    <additionalparam>
      -all -hide java.*
      -collapsible -horizontal
      -inferdep -inferdepinpackage -inferrel
      -outputencoding UTF-8
    </additionalparam>
    <doclet>org.umlgraph.doclet.UmlGraphDoc</doclet>
    <docletArtifact>
      <groupId>org.umlgraph</groupId>
      <artifactId>umlgraph</artifactId>
      <version>5.6.6</version>
    </docletArtifact>
  </configuration>
</plugin>
```
