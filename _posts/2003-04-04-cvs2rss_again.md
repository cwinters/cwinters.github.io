---
layout: post
title: "cvs2rss, again"
---



<a href="/raw/cvs2rss-0.01.tar.gz">cvs2rss</a> - Announcing the first version of a standalone set of scripts to catch CVS commits as they come in and put them in a format we can quickly grab later for generating RSS feeds. It's easy to setup and since you're not trawling the repository for metadata you can run it as often as you like.

<p>To do this, I pulled out the OpenInteract-specific pieces of the package I mentioned here a <a href="/2003/02/26/cvs_to_rss.html">little while ago</a> and modified it to use a <a href="http://www.sqlite.org/">SQLite</a> database rather than a heavyweight RDBMS. It's a little more verbose than some people would probably write themselves, but it seems to get the job done.</p>

<p>One note: I don't use a feed reader, so I have to assume that <tt>XML::RSS</tt> is working properly and the generated feed is valid. If you find otherwise please let me know.</p>


