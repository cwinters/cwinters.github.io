---
tags: java
layout: post
title: "Learning to use dynamic mocks"
---



<a href="http://blogs.atlassian.com/rebelutionary/archives/000083.html">Mike's post</a> last week about dynamic mock objects neatly coincided with new research into testing strategies. At first I couldn't quite understand how the things were working. Mike's example was fairly straightforward, but for some reason the relationship between the controller and the object you actually use in your tests didn't click for a while. Maybe it's because this functionality is merged into a single object in a <a href="http://search.cpan.org/author/CHROMATIC/Test-MockObject-0.12/">Perl implementation</a> (fun with AUTOLOAD...), I dunno. Maybe pair programming would have been useful for this, another set of eyes and all. 

<p>Anyway, eventually it clicked. Once I started writing a few tests -- using <a href="http://www.easymock.org/">EasyMock</a> instead of the dynamic implementation in the <a href="http://www.mockobjects.com/">MockObjects</a> framework -- it seemed very klunky at first. But it really forces you to decompose your interfaces and respect the authority of the <a href="http://c2.com/cgi/wiki?LawOfDemeter">Law of Demeter</a>. I'm still playing, but it's starting to feel more natural.</p>

<p>I still need to write up how we translate scenarioed objects and diffs from XML hierarchies into an HSQL database for testing.</p>


