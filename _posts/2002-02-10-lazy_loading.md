---
tags: perl
layout: post
title: "Lazy loading"
---



<p>I think we should rename the action of 'lazy loading' to 'Just In Time' so we can impress management types :-)</p>

<p>So: version 0.03 of <tt>Class::Factory</tt> (winging its way around CPAN) supports JIT loading of factory implementations.</p>

<p>Hacking on various OI2 pieces is going well -- the change the <tt>Class::Factory</tt> came about from work on the new-and-improved management interface. Instead of the monolithic oi_manage script which performed all the work or delegated where necessary, there's now an <tt>OpenInteract::Manage</tt> interface and task factory. Every task is a separate class that just has to implement <tt>run_task()</tt>, and can optionally implement <tt>setup_task()</tt> and <tt>tear_down_task()</tt> if it wants to do so.</p>

<p>Additionally, there are two main types of tasks: tasks operating on websites and tasks operating on packages. So all of the common setup/tear_down work can be done in these and the task class can focus on what it needs to do. </p>

<p>This should be just a <b>bit</b> more flexible and extensible than the current method, which is pretty much in the "if x gets hit by a bus..." vein.</p>

<p>I'm also trying (and mostly succeeding) in writing tests for many items as I go along. At least the parts that don't require a web server yet -- configuration files, packages, package repositories, context, etc. Nice.</p>




<p><em>(Originally posted <a href="http://use.perl.org/~lachoy/journal/2754">elsewhere</a>)</em></p>


