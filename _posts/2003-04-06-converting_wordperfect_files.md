---
tags: technology
layout: post
title: "Converting WordPerfect files"
---



<a href="http://libwpd.sourceforge.net/index.html">libwpd</a> - Library for importing/exporting WordPerfect v6-v10 files. Found this while glancing at OpenOffice foo. My main interest is modifying the following process:
<ul>
 <li>Get a file created in WordPerfect 5.1 (no joke)
 <li>Open the file in WordPerfect 8
 <li>Use 'Internet Publisher' to save as HTML
 <li>Run the HTML file through a Perl script which tries to chunk out the content into 50 self-contained chunks, tagging each with a title and section along the way.
 <li>The WP5.1->WP8.0->HTML conversion isn't seamless, so a little manual editing is required, mostly to let the Perl script know where a new chunk begins.
</ul>

<p>It's hugely brittle, but it only takes about 20-30 minutes or so to do the conversion, do the parsing, upload the results to a website and reindex them. And it only happens once a month. But still...</p>


