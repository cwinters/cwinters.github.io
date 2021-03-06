---
tags: programming
layout: post
title: "Very strange error about oversubscribing"
---



So I'm plowing through a new subsystem that hooks up with a scheduler (<a href="http://www.part.net/quartz.html">Quartz</a> for now, more on that later). The subsystem needs to read some configuration information from an XML file (yeah, <a href="http://www.cwinters.com/programming/yapc-2003-lt-ini/11.html">I know</a>). The first time I had an error in the document initialization (copy-and-paste error, doh!) so I fixed that and re-ran 'maven deploy'. 

<p>The thing about build systems is they can abstract you from what's going on. Most of the time this is a good thing: who wants to know all that stuff? And maven in particular strongly encourages you to create lots of little subprojects, each with one or just a few closely related purposes. This is also a good thing. But I'd forgotten that the directory from which I 'deploy'ed wasn't creating an EJB artifact (maven lingo). It just created a normal library that got deployed to the JBoss server <tt>lib/</tt> directory. These are not hot deployable.</p>

<p>So after deploying it I re-ran my script script to ping my session bean and kick off this whole process which reads the XML file mentioned above as part of its operation. And I get this error:

<p><pre class="sourceCode">
2003-07-16 15:26:55,483 ERROR [...] Problem reading XML document of field mappings
java.util.zip.ZipException: oversubscribed dynamic bit lengths tree
        at java.util.zip.InflaterInputStream.read(InflaterInputStream.java:140)
        at java.util.zip.InflaterInputStream.read(InflaterInputStream.java:105)
...
(followed by lots of xerces whining)
</pre>

<p>Oversubscribed WHAT? This completely threw me for about ten seconds, like a fistfight breaking out in a Starbucks or something. After my shock I realized it was because of the issue mentioned above: I'd yanked the expected JAR out with the XML document and replaced it with a Folgers brand that didn't agree.</p>


