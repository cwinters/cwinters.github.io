---
tags: java javascript
layout: post
title: "Missing 'load' from Java 6 JavaScript?"
---



<p>The <a href="http://mozilla.org/rhino/">Rhino</a>  JavaScript interpreter has a built-in <tt>load()</tt> function that takes a path to another JavaScript file and imports all its symbols. Very useful for even rudiemtary organization</p>

<p>But I could find neither hide nor hair of such a think in the Java 6 implementation of Rhino. And looking through the <a href="http://download.java.net/openjdk/jdk7/">source for Java 7</a> I saw nothing either. Did this not get brought along?</p>

<p>(BTW, how cool is it that I can now just download the full source for Java, including all the internal Sun implementations? Kick ass, <b>finally</b>.)</p>

<p><b>Update</b>: <a href="http://blogs.sun.com/sundararajan/entry/scripting_updates">it ain't in there</a>


