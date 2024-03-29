---
tags: perl
layout: post
title: "Frameworks and daily use"
---



<p>One of the issues I've found with writing OpenInteract and SPOPS
(both frameworks) is that I tend to use them in the ways that I use
them. (Duh!) So the deficiencies others might see with a process have
been in one of my many blind spots for some time. </p>

<p>For instance, I hadn't originally considered SPOPS to be something
you'd use to write little scripts -- little scripts could use DBI
directly or some other simple method. But little by little, without
realizing it, I've created various shortcuts (or better, the
<b>means</b> for shortcuts) so that such a thing is possible. One of
the <a href="http://www.perlmonks.org/">Perlmonks</a> regulars
mentioned he was interested in SPOPS and pinged me with a little
script he created to scour a directory tree for MP3 files, read the
info and save the info to a database as an object. In running it by
me, he asked, "Can't I just specify the database connection info in
the object configuration?"</p>

<p>I'd never thought about doing this before because I tend to use
SPOPS with lots of objects where centralizing this information in a
superclass makes more sense for maintenance and connection
conservation. But once I thought about it for a minute, I knocked off
a simple behavior to allow you to do exactly what the person asked
for. Sweet. And then I thought about ways it could be easily enhanced
(e.g., do genre checking against a CDDB, etc.)</p>

<p>So I'm going to try to scout out little (or big) tasks like this that
not only might be done easily but that are also ripe for adding nifty
functions easily.</p>


<p><em>(Originally posted <a href="http://use.perl.org/~lachoy/journal/1965">elsewhere</a>)</em></p>


