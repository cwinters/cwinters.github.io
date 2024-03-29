---
tags: perl
layout: post
title: "Framework as CGI, error reporting scheme"
---



<p>Well, the framework has been up and running as CGI on NT.
It's just such a waste that it makes my spine cringe every
time I think about it. Oh well. At least when they start
doing some real work on that machine, we have an upgrade
path for them (PerlEx to the rescue!).

<p>Finally figured out what I think is a decent error
reporting scheme between SPOPS and the framework. Before,
SPOPS would <tt>die</tt> with a hashref with various pieces
of information inside it. All fine and good, and sets things
up for in the future calling <tt>die</tt> with an object
instead (Alzabo has stuff setup like this, altho I don't
know how well it works.)

<p>However, the problem comes when you've got a eval {}
wrapped around something that could be setting $@ to either
a hashref or the normal string. Uh oh. Fortunately, the
mod_perl guide comes to the rescue, courtesy of the
ever-present Matt Sergeant. In it you see how to override
the <tt>CORE::die</tt> function in perl and wrap your own.
Neat, I thought, just check to see if <tt>$@</tt> is a
hashref and if not, put it inside one. Then everything
checking the results of an eval {} can expect a hashref. 

<p>Of course, silly me forgets about the various CPAN
modules being used. They certainly can't be expected to
check whether <tt>$@</tt> is a hashref or not. It's possible
to overload the stringify 'operator' so that evaluating
<tt>$@</tt> (the hashref) in a scalar context actually
returns what's in <tt>$@-&gt;{error}</tt>. But that's a
little too much mucking about in the base expected behavior
for me, particularly for something I'd like other people to
use :)

<p>So, I'm simply going to have all the SPOPS classes and
objects set error information in a common package which
anyone can inspect as needed. And on an error, they'll
<tt>die</tt> with a simple scalar. And everyone will be
happy.

<p>Lesson learned: keep simple things simple.

<p>

<p><em>(Originally posted <a href="http://www.advogato.org/person/cwinters/diary.html?start=6">elsewhere</a>)</em></p>


