---
tags: perl
layout: post
title: "Compile-time implementation enforcement... in Perl"
---



<a href="http://search.cpan.org/~mschwern/Class-Virtual-0.04/">Class::Virtual</a> - This is old news (first released almost <b>three</b> years ago) but it's new to me. (Or I learned it at one time and erased all traces from my noodle.)

<p>The distribution actually comes with two classes. The eponymous one does <b>runtime</b> checking -- it provides for a report on what methods the abstract base class wants subclasses to implement and a nicer error message. The other, <tt>Class::Virtually::Abstract</tt> provides for <b>compile-time</b> checking, which is the real carrot here. The only caveat is that you need to <tt>use</tt> the module instead of <tt>require</tt> it (or <tt>eval "require"</tt> it). Extremely useful  for framework and other library authors.</p>


