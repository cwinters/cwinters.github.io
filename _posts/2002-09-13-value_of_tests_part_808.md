---
tags: perl
layout: post
title: "Value of tests, part 808"
---



I recently added tests for the various export implementations for version 0.69 of <a href="http://search.cpan.org/author/CWINTERS/SPOPS-0.69/">SPOPS</a>, but got bitten -- again! -- by the hash-keys-sort-differently change in 5.8. And about 12 hours after releasing to CPAN I got an automated email from one of the CPAN testers outlining a failed due to not declaring <a href="http://search.cpan.org/author/MSERGEANT/Time-Piece-1.07/">Time::Piece</a> as a dependency. And then an email on one of the mailing lists with this and the aforementioned 5.8 error. Double doh!

<p>On the plus side, it's very reassuring to have more coverage with the additional tests. I only have the import implementations and security to go before all classes are covered. I need to revisit some of the older tests to expand their method coverage, but still.</p>

<p>One of the nice side effects of writing tests is that you are often forced to simplify your interface. For instance: security. In SPOPS you need to have users, groups and security objects defined in addition to the object you're actually protecting. Creating dummy implementations of these isn't hard (esp. with recent additions to <tt>SPOPS::Loopback</tt>), but I have additional functionality required for the security object in particular. Then it hits me: why not just create implementation superclasses so people don't have to keep copying the examples? That was a real forehead smacker... So I'm in the middle of putting that stuff into separate implementation files, documenting it, and <b>then</b> I can use the loopback objects for security. Cool.</p>


