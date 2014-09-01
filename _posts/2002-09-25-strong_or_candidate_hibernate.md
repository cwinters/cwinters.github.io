---
layout: post
title: "Strong O/R candidate: Hibernate"
---



Thanks to a <a href="http://radio.weblogs.com/0100190/2002/09/23.html">pointer</a> from Charles, I took a good look at <a href="http://hibernate.sourceforge.net/">Hibernate</a>. This looks fantastic! It's sufficiently low-level and doesn't try to do everything, has pluggable implementations for keys, and is able to hook up to all the different services (caching, transactions, JMX, etc.) that persistence needs. I don't need to have different objects living on the client and server and I can continue to use the current code generation scheme.


