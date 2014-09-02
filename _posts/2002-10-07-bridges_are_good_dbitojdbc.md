---
tags: perl
layout: post
title: "Bridges are good: DBI-to-JDBC"
---



<a href="http://search.cpan.org/author/VIZDOM/DBD-JDBC-0.64/">DBD::JDBC</a> - A Java proxy allowing you to use Perl's DBI interface along with a JDBC driver to access a database. I had no idea this even existed -- this makes some of my current work much, much easier to test. If you're using it with the current version of DBI you'll need to comment out any references to the DBI <tt>SQL_BIGINT</tt> constant in the Perl module interface since that's been deprecated, but that's a piece of cake. Sweet!


