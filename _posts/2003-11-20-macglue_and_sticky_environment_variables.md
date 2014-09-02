---
tags: mac
layout: post
title: "Mac::Glue and sticky environment variables"
---



Pudge has been <a href="http://use.perl.org/~pudge/journal/15885">posting</a> <a href="http://use.perl.org/~pudge/journal/15894">recently</a> about nifty stuff you can do with the <a href="http://search.cpan.org/~cnandor/Mac-Glue-1.15/">Mac::Glue</a> Perl module. Must investigate further, automation is fun.

<p>In particular he's taken care of a problem I <a href="/2003/11/17/getting_xemacs_working_with_panther_on_the_albook.html">referenced earlier</a> wrt SSH agent environment variables not being populated when you startup the native (or sorta native) <a href="http://members.shaw.ca/akochoi-emacs/">distribution</a> of emacs. His automation creates an SSH agent at startup and fills up the <tt>~/.MacOSX/environment.plist</tt> file with the relevant information. Emacs can read this just like a shell initialization file (e.g., <tt>~/.bashrc</tt>). Cool.</p> 


