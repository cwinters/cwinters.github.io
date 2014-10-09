---
title: "Some 'Superpowers' I've seen, part 2 - Learn your database"
layout: post
tags: database
---

Nearly every application needs to store persistent state, and most of them do
so in relational databases. There's an attitude among many developers that this
database should be treated as a dumb datastore -- speak to it only through an
ORM and use only lowest-common-denominator features.

The reasons for this are many, but they don't really matter.(1) That the
attitude is so widespread is good news for you, because with only a little
effort you can work what looks like magic.

Note that I'm very, very far from a database expert, so if you're looking for
deep performance tuning guidance or query optimization, look elsewhere. . I've used them for a while,
and understand some basic use patterns

## Learn how your database works.

Time spent optimizing your database interactions will pay off 10x (or more)
than time spent optimizing your code. This also means you need to learn how to
listen to what your database is telling you -- monitoring, statistics
gathering, logging, etc.

A nice thing about this: it doesn't change as often as other aspects of our
world. And some of the things you learn -- like about column ordering in
indexes -- are often applicable across vendors.

(What is this? See [Part 1](/2014/09/19/documentation-superpower.html))

---
(1) Well... my over-beer opinion is that that four things are the the source
of this. (1) Not wanting to deal with DBAs (large company-specific), (2) ORMs 
and dissonance between set-based (relational) and OO mindsets, (3) MySQL, and 
(4) Frameworks (like Rails) that strive for database independence and are first 
built on MySQL, so they start out with the assumptions of a lowest-common-denominator
solutions which are hard to undo later. IIRC, if you ply him with a beer
[@theory](http://twitter.com/theory) will probably issue a good rant or five on this...


