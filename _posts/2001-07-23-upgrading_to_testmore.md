---
tags: perl
layout: post
title: "Upgrading to Test::More"
---



<p>Released new versions of <a href="http://www.advogato.org/proj/OpenInteract/">OpenInteract</a> (1.1)
and <a href="http://www.advogato.org/proj/SPOPS/">SPOPS</a> (0.41) on Friday and didn't get any
angry emails over the weekend, which is a good sign. I also
modified all the testing scripts to use <a
href="http://search.cpan.org/search?dist=Test-More">Test::More</a>,
which is quite simple but quite useful. It's funny how it
started -- Thursday night I was surface-cleaning up docs,
making sure all the POD was manified without errors and
figured I should add a test (or two) for iterators.

<p>It was like unraveling a threadbare rug -- one tug on one
strand and the whole thing started falling apart. (Well,
maybe not that dramatic, but still.) So, remembering the
talk from YAPC I nabbed the aforementioned module and
started converting. It's an additional download for people,
but it's pure Perl so it shouldn't prove problematic. On top
of that, I modified the tests to use some of the shortcuts
written recently, so overall writing tests is easier now.
This is definitely good.

<p>I'm thinking I should move the SQL data moving
abstraction stuff from OpenInteract to SPOPS. At the least
it would make it easy to specify tables and data for testing
:-)

<p>Went to Erie (Pennsylvania) on Sunday to hang out on the
beach with my wife and mother-in-law. Very pleasant. Not
much work done over the weekend, but that's not necessarily
a bad thing.

<p>Also in the process of building a new gateway from my old
workstation parts. Most everything is installed and running
ok, just need to copy my OpenInteract configuration and
theme stuff from the (very) old version on MySQL to the
newest version on PostgreSQL. Also going to setup IMAP
(using Cyrus) since mutt's IMAP support is pretty decent,
and then something like <a
href="http://astray.com/acmemail/">acmemail</a> for
web-based access, since checking email from Greece a few
weeks ago was a PITA.

<p>
<p><em>(Originally posted <a href="http://www.advogato.org/person/cwinters/diary.html?start=62">elsewhere</a>)</em></p>


