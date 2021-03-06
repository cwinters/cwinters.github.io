---
tags: niagara orm vacation
layout: post
title: "Visiting Niagara, SPOPS triggers"
---



<p>Good and bad news of late.

<p>First, this past weekend we went camping with Barb's
aunt, uncle, mom and my sister around Erie, Pa. On the way
there, we realized that Niagara Falls was only (in theory)
about an hour away, so we figured what the heck.

<p>Took a little longer than that, and it was crowded as all
get out, but pretty amazing. I'd like to go when the weather
isn't so great (colder, which will probably happen in about
three weeks or so...), there are fewer people and it's
easier to get lost in the sound and fury without some
screaming baby or whatnot. Fun trip overall, though.

<p>Another good thing: got through a nice little idea
barrier last night and implemented some nifty stuff in
SPOPS. Kindasorta like triggers in a DBMS, we can make it
really easy to apply all sorts of disparate metadata layers
on the data objects. For instance, restricting certain data
objects to certain groups; allowing users/groups to
'publish' the data object and other users/groups to
'subscribe' to all objects or even those that meet certain
criteria. The cool thing is that you can have any number of
'rules' (term for now) applied to two phases of an action --
for instance, when you call 'save', you can create a rule
for before the object is saved, and after the object is
saved. Ditto with 'fetch' and 'remove'. Cascading deletes
are now really simple, as is lots of other interesting
stuff.

<p>The only thing I hate about getting over a hump like this
is that I look back at the hurdles I couldn't previously
jump over (or go around) and think "Duh!" and get down on
myself for not seeing it earlier. But I suppose that's
inevitable (and almost always not prolonged).

<p>Bad news: encountering unexpected resistance in
opensourcing OpenInteract and SPOPS. Enormous downer. It's
not done yet, and I think with a good argument we will be
able to release SPOPS and the crucial parts of OpenInteract.
I'm working on that now. I'm proud of all the work that's
gone into this, and I want to be able to share it and see
people doing things I never dreamed with it.

<p><em>(Originally posted <a href="http://www.advogato.org/person/cwinters/diary.html?start=15">elsewhere</a>)</em></p>


