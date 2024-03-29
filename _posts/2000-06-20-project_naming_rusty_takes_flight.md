---
tags: perl
layout: post
title: "Project naming, Rusty takes flight"
---



<p>SPOPS are fairly settled now, security and all. And the
web application framework is coming along very nicely as
well. I hope to get it implemented on <a
href="http://www.cwinters.com/">my website</a> soon (next
week), but these things have a way of not working out.

<p> <p>Side note: how the heck to people come up with clever
names for projects? Right now the framework is just "the
framework", or sometimes "Interact Application Framework."
(IAF isn't bad, because then the programmers can be the
"Interact Application Force".) But it seems like you either
think of something clever early (I like the name of <a
href="http://sourceforge.net/project/?group_id=2601">Jellybean</a>)
or not at all.... Or maybe it's just me :)

<p>Anyway: the framework. Basically, a lot of the admin
crap that is assumed to be in a framework -- users, groups,
templating schemes, error handling, themes and a consistent
output scheme -- is working and working solidly. Security on
a per-object and a task basis is also working ok. (Don't
know how it will scale, but...) Creating content handlers is
a fairly simple process, and enabling security in a content
handler is a matter of putting a certain class in your
<tt>@ISA</tt> and setting a minimum security level for each
publically accessible method.

<p>Caching works, but not in as nice a fashion I'd like.
And some things can almost certainly be tightened -- that's what
happens when only one person works on the code. (Oh, did I
mention that punk <a
href="http://www.kuro5hin.org/?op=displaystory;sid=2000/6/7/151425/7439">Rusty</a>
is leaving us to go to <a
href="http://www.opensales.org/">OpenSales</a>?) ("Punk" in
the nicest sense of course :) For
caching, it would probably be a good idea to look into how
Mason does it. I believe that everything is a component, and
the parent <tt>Mason::Component</tt> class takes care of
caching. The only wrinkle in this is, of course, themes. And
you don't want to cache something that has any specific
distinguishing items in it -- error messages, for example :)

<p> <p>I had a chuckle yesterday when I typed in the wrong
password for monster.com -- I got a totally blank screen
except for "You typed in the wrong password. Please try
again." in big letters at the top. They're running superbowl
commericials and I've got better error handling!

<p>Really looking forward to <a
href="http://www.yapc.org/America/">yapc</a> again this
year. Except this year I don't have to be all worried about
my presentation :)

<p><em>(Originally posted <a href="http://www.advogato.org/person/cwinters/diary.html?start=3">elsewhere</a>)</em></p>


