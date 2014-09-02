---
tags: java
layout: post
title: "Little inconsistency in tag files"
---



Our new application/module will be deployed under Tomcat 5 or any other suitable JSP 2.0 container<sup>1</sup> so we get to use tag files. They're fairly handy but one thing (so far) is pretty annoying. You declare inbound information via <tt>attribute</tt> tags and outbound information via <tt>variable</tt> tags. The default class for each is <tt>java.lang.String</tt>, which is fine -- normally webapps just sling around strings. But to change the default class you set the <tt>type</tt> attribute in <tt>attribute</tt> and the <tt>variable-class</tt> for <tt>variable</tt>. Huh? Didn't anyone use this before implementing it?

<p><sup>1</sup> Yes, Tomcat. Get over it.</p>


