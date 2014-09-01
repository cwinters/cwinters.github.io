---
layout: post
title: "More new versions"
---



<a href="/~merlyn/">Merlyn</a> pointed out, again, that the version numbering for modules in SPOPS were retrograding with version increases. The problem was that I used a crappy CVS Revision formatter which treated '2.7' as '2.70' rather than '2.07'. Thanks to the CPAN testers, I also found that one of my tests failed on 5.8 because I was (one step removed) relying on hash key order. So 0.67 and 0.68 went out in short order, just after releasing 0.66 earlier this week. Doh!

<p>
<p><em>(Originally posted <a href="http://use.perl.org/~lachoy/journal/7392">elsewhere</a>)</em></p>


