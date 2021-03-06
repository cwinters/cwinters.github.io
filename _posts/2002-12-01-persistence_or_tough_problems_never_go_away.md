---
tags: java
layout: post
title: "Persistence (or: tough problems never go away)"
---



Jon has a <a href="http://roller.anthonyeden.com/page/tirsen/20021129">nice back-and-forth</a> about persistence, ending with <a href="http://www.prevayler.org/index.html">Prevayler</a> getting some props. (<a href="http://radio.weblogs.com/0108103/2002/11/30.html#a114">Joe responds</a> to this as well.) I'd love to use something like this, but every application I've developed needs to be accessible from multiple development platforms -- main application, reporting, data mining, legacy interface, etc. With web services becoming more ubiquitous (and faster!) this could become moot, but AFAICT we're not there yet.

<p>I've <a href="/2002/10/30/beauty_of_pojos.html">said this before</a> but I think the scheme of imposing serialization on objects (top-down) rather than having the objects serialize themselves (bottom-up) is the way to go. Everyone uses the same objects (no value/transfer object) and it's easier to swap out serialization implementations. It also offers much more flexibility -- for instance, you can have a client-side persistence manager that hooks into a simple cache (particularly for stable lookups) and a server-side one that talks to a distributed transaction cache. And if you want, you can even use these POJOs with an in-memory scheme for testing, or even in production with Prevayler or one of its buddies.</p>


