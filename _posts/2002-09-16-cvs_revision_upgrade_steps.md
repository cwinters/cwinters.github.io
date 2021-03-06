---
tags: programming
layout: post
title: "CVS revision upgrade steps"
---



I don't do this often enough to be a pro, so this is partially a note for future reference. Occasionally I'll perform some numbskull maneuvers that exhibit themselves when I upgrade a CPAN module: the new version includes classes that have VERSION numbers older than ones already in the repository. (Somehow, <a href="http://www.stonehenge.com/merlyn/">merlyn</a> always catches these. Magic.) Since I use CVS to generate my version strings, I'll need to tell CVS to upgrade the revision number. This is easy:

<pre>
$ cvs commit -r 2.16 Foo.pm
</pre>

<p>However, this leaves a sticky tag on the file:</p>

<pre>
$ more CVS/Entries
/Foo.pm/2.16/Mon Sep 16 19:53:34 2002//T2.16
</pre>

<p>And if you try to change it and commit it, CVS will give you a nasty warning (which I can't remember right now) and refuse to commit the changes. To fix this you need to remove the sticky tag, which is also easy:</p>

<pre>
$ cvs update -A Foo.pm
$ more CVS/Entries
/Foo.pm/2.16/Mon Sep 16 19:53:34 2002//
</pre>


