---
tags: perl
layout: post
title: "TWiki fun, shared webhosts, SourceForge update"
---



So I found what I thought was a TWiki bug, duly <a href="http://twiki.org/cgi-bin/view/Codev/MultipleContentTypeHeaders">reported it</a> and was pleasantly surprised by a pointer to a fix a short while later. Nice work!

<p>There's an existing TWiki plugin to highlight source code (<a href="http://twiki.org/cgi-bin/view/Plugins/BeautifierPlugin">BeautifierPlugin</a>) but I didn't like how it handled Java code. So I modified it to use <a href="http://www.gnu.org/software/src-highlite/">GNU source-highlight</a>, and then eventually just rolled the changes into <a href="http://twiki.org/cgi-bin/view/Plugins/SourceHighlightPlugin">a separate plugin</a>. Everything worked on the server at work, so I figured I'd just install it on the <a href="http://openinteract.sourceforge.net/">OI Wiki</a> so the Perl code there will look decent.</p>

<p>No good. Actually, that's not entirely true: it's <b>every once in a while </b> good, which is even worse. It works about 10% of the time and bails with an exit code of 127 (or every once in a while a signal 11) the rest of the time. Totally infuriating. It's not a permissions issue, path issue, tainted path issue, program error or anything like that. It just refuses to work most of the time. I suspect it has something to do with the Sourceforge shared webhost: maybe it puts the clamp on CGI processes spawning children processes when the load is above <em>x</em> or the number of processes is above <em>y</em>. Oddly, this is only the second time in my career I've ever been on a shared webhost. The rest of the time I've been an admin of the box. (And the first time doesn't count since I was a newbie.) So I'll have to revert to the BeautifierPlugin for the OI Wiki. Feh.</p>

<p>Creating TWiki plugins is pretty simple, though, and it would be fairly easy to create two-way links between your bug database and a wiki page with something like:</p>
<pre>
You can see an example of this ThreadSyncronization
error at work in %BUG{id="89102" status="true"}%
</pre>

<p>And replace the %BUG...% key with a linked title and status for that particular bug. Lots of possibilities.</p>

<p>Also of note: <a href="http://gforge.org/">GForge</a>, the replacement for people using Sourceforge for internal bug tracking is just about done with version 3.0. It includes tons of cleanup from the SF code, removing lots of SF-specific workarounds and fixes. It also implements a SOAP API, which could be interesting, particularly coupled with a potentially <a href="http://www.intellij.org/twiki/bin/view/Main/NetTasks">useful IDEA plugin</a>. It still uses PHP though, which is a shame.</p>


