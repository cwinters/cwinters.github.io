---
title: "Some 'Superpowers' I've seen, part 2 - Learn your database"
layout: post
tags: database
---

There's an attitude among many developers that the database should be treated
as a dumb datastore. Speak to it only through an ORM and use only
lowest-common-denominator features.

The reasons for this are many, but they don't really matter.(1) That the
attitude is so widespread is good news for you, because with only a little
effort you can work some magic.

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
(1) Oh fine. My over-beer opinion is that that four things are the the source
of this. (1) Not wanting to deal with DBAs, (2) ORMs and relational vs OO
mindset, (3) MySQL, and (4) Frameworks (like Rails) built on MySQL,
particularly back when it was basically a SQL front end on the filesystem. IIRC
[@theory](http://twitter.com/theory) has a good rant or five on this...


