---
tags: programming
layout: post
title: "Counting lines of code"
---



<a href="http://www.dwheeler.com/sloccount/">SLOCCount</a> - A <a href="http://perlmonks.org/index.pl?node_id=289111">Perlmonks post</a> pointed me to this. Previously I'd just used <tt>wc</tt> to get a rough estimate. But that includes POD and other docs and I don't care enough about the figure to create something better. This program filters out comments and seems to work for more than two dozen languages. Cool.

<p>More interesting but of dubious value are some value metrics it generates. Running this program against the <a href="http://cvs.sourceforge.net/cgi-bin/viewcvs.cgi/openinteract/OpenInteract2/">OpenInteract2 source</a> tells me that I have 34,400 SLOC, and using something called a COCOMO model it estimates:</p>
<ul>
 <li>...development time in person years: 8.21</li>
 <li>...schedule: 1.19 years</li>
 <li>...average number of programmers: 6.89</li>
 <li>...cost to develop: US$ 1,109,416</li>
</ul>

<p>Obviously to be taken with a large grain of salt :-)</p>

<p>BTW, the SLOCCount author <a href="http://www.dwheeler.com/">David Wheeler</a> is not the same <a href="http://david.wheeler.net/">one</a> who gave an excellent <a href="/2003/08/26/guest_to_pittsburghpm_next_week.html">presentation on Bricolage</a> on Tuesday. That threw me for a second...</p>


