---
tags: perl postgresql
layout: post
title: "Another small DBD::Pg issue"
---



<p>I bumped into another <tt>DBD::Pg</tt> issue posting that last news item, complaining about an unbound placeholder. That's straightforward enough, but in the SQL dumped to the error message there were no placeholders! A closer inspection showed that the dates weren't quoted -- ouch. (<tt>SPOPS</tt> doesn't use bound placeholders for inserts, instead quoting each value it passes in. I think this was because n years ago <tt>DBD::Sybase</tt> didn't properly bind TEXT datatypes but I'm not sure.)</p>

<p>Anyway, a little investigation showed that the two-argument <tt>quote()</tt> method implemented by <tt>DBD::Pg</tt> does not quote dates properly. The two-argument version takes both the value to be quoted along with the field's datatype ('93' as reported by <tt>DBD::Pg</tt> for a timestamp field). The one-arg version is fine, though, since it just blindly escapes and quotes whatever you give it.</p>

<p>So the workaround was pretty easy: in <tt>SPOPS::DBI::Pg</tt> I just had to override the  <tt>sql_quote()</tt> method from <tt>SPOPS::SQLInterface</tt> to use the one-arg form of <tt>DBI->quote()</tt> when given a timestamp datatype.</p>

<p>And yes, I created a quick test to show this and <a href="http://rt.cpan.org/NoAuth/Bug.html?id=15082">posted it</a> to its <a href="http://rt.cpan.org/NoAuth/Bugs.html?Dist=DBD-Pg">RT queue</a> like a good open source citizen.</p>


