---
layout: post
title: "Easy Perl XML"
---



<p><a href="http://www.advogato.org/person/agntdrake/">agntdrake</a>: The perl module you're
looking for is <a
href="http://search.cpan.org/search?dist=XML-Simple">XML::Simple</a>.
Very (!) easy to translate from a hashref of whatever
(arrays,
hashrefs, scalars) to XML and back again. The only slightly
annoying thing is that it represents almost everything as
XML name keys (<tt>&lt;key name1="val"
name2="val2"&gt;</tt>) versus the way you describe. It's all
valid XML, but one is easier (IMO) to hand-edit than the
other, which is a legit concern when you're using it for
configuration files.

<p><em>(Originally posted <a href="http://www.advogato.org/person/cwinters/diary.html?start=30">elsewhere</a>)</em></p>


