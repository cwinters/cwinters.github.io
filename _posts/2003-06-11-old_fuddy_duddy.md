---
tags: technology
layout: post
title: "Old fuddy duddy"
---



I hate to sound like a geezer, but what's up with skipping three characters (out of six) when expressing colors in hex? I've been putting together my presentation for <a href="http://yapc.org/America/">YAPC::NA</a> and decided that it would be useful to use CSS instead of tables for the layout. (Yeah, I know, only about five years behind...) Another motivation is that I'd like to move the default layout of OpenInteract to this as well.

<p>So in looking at different stylesheets and <a href="http://webreference.com/authoring/style/sheets/layout/advanced/">tutorials</a> you see stuff like this:</p>

<p><pre class="sourceCode">
#level0 {
     background:#FC0;
}
</pre>

<p>and then later on, in the same article:</p>

<p><pre class="sourceCode">
#level2 {
    background:#FFF3AC;
}
</pre>

<p>I'm not totally dense (most of the time) and figured out that the first meant <tt>#FFCC00</tt>, but why create such a shortcut? It may just be that I'm not used to it, but it breaks up of the flow of what I expect. Not seeing the shape of a six-character sequence makes my eyes halt and stop where they really don't need to. And when did this become ok? Whine whine whine.</p>


