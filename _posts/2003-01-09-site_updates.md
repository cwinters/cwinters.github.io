---
tags: perl
layout: post
title: "Site updates"
---



In the continuing spirit of dogfood I've upgraded this site to the as-yet-unreleased OpenInteract 1.56. There are a few very minor changes to the framework, but I've done a bit of work in the last few days to the 'news' package, which controls the blog entries. Changes include finding all the entries in a particular second and/or month/day -- you can see this on the <a href="/news/">main blog page</a>. (You can also keyword search using the input on the navigation bar.) Also, I added the standard previous/main/next links on every individual entry, which was inspired by <a href="http://www.rollerweblogger.org/page/roller/20021229#having_context">David's comment</a> about how blog entries never stand alone. I totally agree.

<p>SPOPS users may want to note: the previous/next links are maintained automatically on object insert using <a href="http://spops.sourceforge.net/doc/SPOPS/Tool/DBI/MaintainLinkedList.shtml">SPOPS::Tool::DBI::MaintainLinkedList</a>. Piece of cake.</p>

<p>I also noticed a problem with the <a href="/new/">what's new</a> listing -- there were no entries after December 29. (It's fixed now, I just added them manually.) Weird. The first crazy thought that crossed my mind was that I had a Y2K+3 bug or something. But it was a subtle programming error introduced by upgrading to SPOPS 0.73 (and subsequently 0.74) and the object state before it calls the post-save rules. But I was happy to find it fairly quickly :-)</p>


