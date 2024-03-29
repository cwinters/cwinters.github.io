---
tags: programming
layout: post
title: "Various shell miseries"
---



<b>Misery #1:</b> Beware single quotes in the Win32 shell!

<p>The modern Win32 shell (<tt>cmd.exe</tt>, how I loathe thee) treats single- and double-quotes differently than the typical Unix shell. How did this bite me? I wrote a quickie Perl script to let a co-worker find all places where one or more of a gaggle of fields were used in a set of stored procedures. Not too tough, and I can continue spread the Perl virus. We write it on my machine, test it out and it works great. I commit it to CVS and we go over to his machine to grab it from CVS and run it.</p>

<p>Except it doesn't work. I'm using the same effing arguments as on my machine but it's not working. I cycle through a number of debugging techniques (which is instructive to my non-Perlish co-worker) but none of them work -- the directory scanner is finding the right files, the file actually has the string to match, it's not case-sensitive. Then I print out what the program is trying to match. And it's got an extra set of single quotes around it, like this: <tt>''MATCH TEXT''</tt>. Dammit! I was using the single quotes to delimit the argument, not to be included in the argument. Bastards!</p>

<p>Change the singles to doubles and everything is peachy. Thanks Microsoft! Future warning: always test in your future environment, as I tested on my machine initially with cygwin, which while a band-aid over gaping MS wounds is still decent.</p>

<p><b>Misery #2:</b> Beware of binary path caching!

<p>In the process of stocking my new Powerbook (status: honeymoon continues) I installed the newest version of <a href="http://maven.apache.org/">Maven</a>, RC1. Everything built on the Powerbook just fine so I decided to see if it would work in our normal environment. Download the ZIP, unpack it and stock the repository like it says, modify my <tt>MAVEN_HOME</tt> and <tt>PATH</tt> environment variables and run it. I get:
<pre class="sourceCode">
$ maven clean.all
java.lang.NoClassDefFoundError: com/werken/forehead/Forehead
Exception in thread "main" 
</pre>

<p>WTF? Okay, maybe the repository didn't get created properly? Nope, it's okay. I specified the right paths in the environment, right? Yep. Okay, maybe it'll work in the dreaded <tt>cmd.exe</tt> (how I loathe thee) shell? Nope, same result. Google around, no joy, just messages about <tt>MAVEN_HOME</tt> not being set, but mine is.</p>

<p>Sneaky suspicion:
<pre class="sourceCode">
$ which maven
/cygdrive/c/java/maven-1.0-beta-10/bin/maven
</pre>

<p>Foiled again! Calling maven with the fully-qualified path works fine. Bad shell for caching the path to the script!</p>



