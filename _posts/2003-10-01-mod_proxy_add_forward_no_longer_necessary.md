---
tags: programming
layout: post
title: "mod_proxy_add_forward no longer necessary"
---



<a href="http://groups.yahoo.com/group/modperl/message/46001">mod_proxy_add_forward.c
</a> - If you've setup an Apache HTTP proxy for your application server [1] then you've probably run into the problem of keeping your addresses straight. That is, since you've got A requesting from B and B requesting from C, how does the heavyweight server (C) know where the original request (A) came from?

<p>If you were using Apache and mod_proxy you could use a tiny little module called <a href="http://develooper.com/code/mpaf/mod_proxy_add_forward.c">mod_proxy_add_forward</a>. This would add the header 'X-Forwarded-For' to the request sent to the application server, which presumably had sufficient hooks to pull out the value and use it for its own request. And for the last so many years this was as much a part of my Apache build process as <tt>./configure</tt>.</p>

<p>Today I needed to set this up but didn't have my usual free rein over compiling the front end server. I needed to compile a DSO instead of just build it in statically as normal - PITA. After fumbling about with it a while, and failing, I went googling and found the above message, the important part of which is:</p>

<blockquote>As you may know then the proxy module in httpd 2.0 incorporates the X-Forwarded-For, X-Forwarded-Host and X-Forwarded-Server functionality of mod_proxy_add_forward.c.</blockquote>

<blockquote>I just noticed that Thomas Eibner got the proxy people to put it into apache 1.3 too since 1.3.25.</blockquote>

<p>How did I miss that? And now that I've contributed some more minutes to the 'needlessly spinning my wheels' bank I'll expect to make a withdrawl, with interest, in the near future...</p>

<p>[1] lightweight http server delivering static content and passing along other requests to a heavyweight http/application server</p>


