---
tags: perl
layout: post
title: "Forking hazardous to database connections "
---



This is something I should have known but I don't write forking servers very often, or use them close enough to the metal to care. But this time I was testing out the <a href="http://search.cpan.org/author/GAAS/libwww-perl-5.69/lib/HTTP/Daemon.pm">HTTP::Daemon</a> interface for OpenInteract 2 (which is nearing beta, more soon). This allows us to run OpenInteract entirely standalone, as opposed to running it inside Apache using mod_perl or (god forbid) as a one-off CGI process. It's not going to break any speed records, but it makes for a great <a href="http://www-3.ibm.com/ibm/easy/eou_ext.nsf/Publish/626">OOBE</a> and is also extremely useful for testing :-)

<p>So the server started fine but I kept getting the following error:</p>

<p><pre class="sourceCode">
DBD::Pg::st execute failed: server closed the connection unexpectedly
</pre>

<p>And I couldn't figure out what was going on. The same code worked fine in Apache, worked fine in CGI. So what's up?</p>

<p>The thing is, when the server starts up OI2 creates a database connection so we can read metadata from the tables and use it to create the persistence classes on the fly. (Using <a href="http://spops.sourceforge.net/">SPOPS</a>, naturally.) This is done in the parent.</p>

<p>We then fork off a child to handle incoming requests. Children inherit all the parent data structures, but some 'live' structures (sockets, database connections, etc.) don't make the transition. So there was an entry in the datasource manager referring to the parent's live database connection, but there was no longer a connection there. Thus, the message. Forcibly closing all database connections before forking fixed the problem -- each child reconnected on its own and happily served up requests. But the googlespace on the message was no help at all, so here's a potential nudge...</p>


