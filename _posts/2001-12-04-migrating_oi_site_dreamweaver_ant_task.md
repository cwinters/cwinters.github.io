---
tags: programming
layout: post
title: "Migrating OI site, Dreamweaver, Ant task"
---



<p>Late, late night -- first in while. I've discovered it's
an amazingly effective cure for having too many emails in
your box when you wake up.

<p>Upgraded the <a href="http://www.ctaa.org/">major
site</a> -- which was actually at 1.1 instead of 1.2 -- to
<a href="http://www.advogato.org/proj/OpenInteract/">OpenInteract</a> 1.36. It went very well, IMO.
(Jury's still out I suppose, but I've got a good feeling and
those can normally be trusted.) Aside from a stupid error
that cost ~30 minutes early on, that is.

<p>I'm also going to be releasing packages that get updated
between releases to the <a
href="http://sourceforge.net/projects/openinteract/">Sourceforge
site</a>. And now that I've got these extra packages
working, they'll be going up as well.

<p>I've been messing about with Dreamweaver at the office
(thru VNC of course) to write an extension for the damned
image rollovers. DW comes with an extension for this, of
course, but it doesn't play nice with <a
href="http://xmlc.enhydra.org/">XMLC</a> -- since customers
may be updating the pages themselves, each page really has
to be a drop-in no-brainer. The image tags and javascript
generated by the DW default rollover extension makes this
impossible.

<p>I've modified an <a
href="http://jakarta.apache.org/ant/">Ant</a> custom taskdef
that came out of Enhydra (at some point) to make for
flexible URL mappings and such, so these rollovers are (I
think) the last hurdle to jump.

<p>Extending DW is pretty nifty, once you get the hang of
it. Representing the document being edited is smart,
although the method of text replacement is amazingly clunky.
 Still, I'm impressed.

<p><em>(Originally posted <a href="http://www.advogato.org/person/cwinters/diary.html?start=88">elsewhere</a>)</em></p>


