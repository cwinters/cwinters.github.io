---
tags: java
layout: post
title: "Code generation"
---



<p>I'm revisiting the system used to generate lots of Entity and Session beans for the system at work. It uses a Java class to dump JDBC metadata to a file, then a series of Perl clases that use this data metadata, human-entered relationship and usage metadata, and s series of Template Toolkit templates to generate lots of Java source and the necessary XML deployment descriptors. (Huh, maybe I should have submitted <b>that</b> to OSCON...)</p>

<p>It works pretty well right now, but my reasons for revisiting are:</p>

<ul>
  <li>20% allowing someone else to edit the relationship/usage metadata (currently in one big serialized perl data structure, going to be in separate INI files)</li>
  <li>40% to extend it to create the classes necessary to implement the Business Delegate pattern and make the Entity beans "dumber", and</li>
  <li>40% to simplify it, so that I can understand it when I look at it in six months :-)</li>
</ul>

<p>I toyed with the idea of rewriting it in Java so the system would be more homogenous (and I'd get some experierience with Java templating systems) but there's not enough time for that.</p>


<p><em>(Originally posted <a href="http://use.perl.org/~lachoy/journal/3666">elsewhere</a>)</em></p>


