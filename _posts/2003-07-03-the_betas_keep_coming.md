---
tags: programming
layout: post
title: "The betas keep coming"
---



I <a href="http://mathforum.org/epigone/modperl/khimgangnu">released</a> the new OpenInteract 2 beta this morning: beta 2 == 1.99_01. Lots of good stuff in this, including the <a href="/2003/07/01/hitting_your_stride.html">aforementioned</a>  content filters and new content generation plugins. Logging is totally rewritten (using log4perl). The docs aren't completely done (in particular info on authentication and the package development tutorial), but the quickstart guide was put into its own area and built up, caching is now explained in detail, and a number of other areas in the manual and in the package docs themselves are fleshed out. I noticed a few documentation errors after release but that always happens. I'll have to make sure it works with the <a href="http://mathforum.org/epigone/modperl/tandspixrar">just-released</a> mod_perl 1.28 as well.

<p>I think in one or two more betas I'll move my own site over to it -- if only so I can create the data migration tools for other people to do the same thing...</p>

<p>Once you start an explicit beta cycle I think it's important to keep releases coming in fairly short order, three or four weeks or so between iterations. (More is okay for large -- Mozilla large, that is -- projects.) Not only does it give the appearance of lots of work happening (which clueful users can quickly see through if they're empty releases, so don't get any ideas), but it prevents you and your team from going feature crazy. Adding too many features between betas is a big disincentive for those users who are interested in following along, installing each beta as it comes out. True, you don't want to get hamstrung by backwards compatibility to a beta release, but you also want to keep these people happy because they're your best friends. They're the ones who come up with easier ways to do things, dream up new features that are often simple to implement, let other people know in forums and mailing lists about the work that's going on. They also notice embarrassing typos in your docs :-)</p>

<p>One of the beefs I have with many Java projects is that they take too far too long to put out releases. How long was <a href="http://jakarta.apache.org/struts/">Struts</a> in beta? Struts is not that complicated, there is <b>no way</b> it should have taken more than two or three months. Plus the differences between the 1.0 and 1.1 releases were <b>huge</b>, but you wouldn't know it from the version number. Release early, release often.</p>

<p>And how long does <a href="http://maven.apache.org/">Maven</a> (which I'll write about more shortly) take between beta releases? And it's not even to 1.0 yet! While it's a complicated build tool, it's still just a build tool. When a user asks about a new feature and you answer, "It's in CVS," and you're in a beta cycle, you should always be following that up with, "and it'll be out in a couple weeks with the next beta." If you're answering, "Just download the snapshot" for more than a couple of weeks then something is wrong. And when you have a <a href="http://wiki.codehaus.org/maven/BrokenManifestInBeta9">serious bug</a> you need to put out a new release, right now.</p>



