---
tags: programming soap design simplicity complexity
layout: post
title: "Programming by coincidence"
---



<p>A little while ago I was wrestling mightily with SOAP and 
<a href="http://twitter.com/cwinters/status/1245461128">posted</a> 
this on twitter:</p>

<blockquote>
every time I do anything nontrivial in SOAP I resort to
programming by coincidence, and I really hate it
</blockquote>

<p>One of my coworkers requested a clarification on what I meant
and I 
<a href="http://twitter.com/cwinters/status/1248749724">summed up</a> 
as best I could given the space:</p>

<blockquote>
by coincidence: A might work, try it! no? B might work, try it!
no? C might work...
</blockquote>

<p><a href="http://www.pragprog.com/the-pragmatic-programmer">The Pragmatic Programmer</a>
has a good deal to say on this, but the related tip will do for now:</p>

<blockquote>
<b>Don't Program by Coincidence</b>
<br />
Rely only on reliable things. Beware of accidental complexity,
and don't confuse a happy coincidence with a purposeful plan.
</blockquote>

<p>When we talk about elegant systems we usually extol the
virtues of componentization: the idea of writing applications by
putting lego-like pieces together has been around for probably as
long as software itself. And a lot of times that works swimmingly
(see CPAN).</p>

<p>However, one area where this breaks down is when you're using
a fairly complex component that itself wraps up a whole bunch of
other components. The most common case is with frameworks.</p>

<p>In this case, it was 
<a href="http://cxf.apache.org/">Apache CXF</a>. Don't get me 
wrong, I think CXF is a great piece of
software. It has decent documentation, excellent integration, a
very responsive developer community, and the benefit of being a
rethink of earlier projects.</p>

<p>But there is a <strong>lot</strong> of software assumed when
you say "CXF". Its <tt>lib/</tt> directory has 65 separate JAR
files. They're almost certainly not all necessary for your task
-- in fact, there's a very helpful <tt>WHICH_JARS</tt> file in
that directory to tell you which ones you need for which use
cases.</p>

<p>My use of CXF is pretty plain vanilla. And because it's not
central to our application I don't know it that well -- in fact,
I want to know as little as possible to get it working. [1] And
this is where we run into some tension.</p>

<p>Understanding SOAP top-to-bottom involves a huge number of
fairly complex technologies, WSDL, XML Schema, databinding and
code generation tools chief among them. You can spend many solid
weeks really understanding each of these just by themselves, and
even longer on how the different software packages implement and
internalize them. And when you stack them on top of one another,
and you're not sure which layer is generating error messages, or
if you're wiring them together properly? Ouch.</p>

<p>I'm not arguing against anything except complexity, which is
kind of like arguing against river floods or crushed puppies. But
such complexity should be an indication when we build these
software stacks that something is deeply wrong. Because software
is supposed to help us manage the complexity of our lives, not
add to it. Most domains have enough 
<a href="http://97-things.near-time.net/wiki/simplify-essential-complexity-diminish-accidental-complexity">essential
complexity</a> that using such stacks just make things
worse. This is one of the reasons so many people reinvent such
frameworks (and even the components used), because they're trying
to impose a consistent worldview from top-to-bottom, so people
won't have to resort to coincidences to get things done.</p>

<hr noshade="noshade" />

<p>[1] This isn't true for all such projects -- with some (like
<a href="http://jersey.dev.java.net/">Jersey</a>) I'm actually
interested in understanding how the project views the world and
solves problems.</p>



