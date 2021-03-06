---
tags: ide scm standards
layout: post
title: "Hooray for standard formats!"
---



<p>IDEA 7 has a nifty feature called 'Shelve changes'. Some SCM
systems have this -- it's the ability to take a set of changes and
have the SCM 'forget' about them so you can do other work independent
of them. You can then reintegrate them back in one fell swoop. The
typical use case is to move aside changes for a big feature to
implement one or more small features at the same time so you don't
accidentally bring the 'big feature' changes in with the small ones.</p>

<p>(From what I understand this is built-in to most distributed SCM
systems -- branches aren't the heavyweight things they are in
Perforce, so every feature becomes its own branch and has its own
changesets associated with it. Cool.)</p>

<p>Anyway, somehow IDEA lost track of a shelf I'd made a week or two
ago -- I hit Alt-9 to see the changes, then Alt-RightArrow twice to
the see the 'Shelf' tab, only to see there was no 'Shelf' tab. Shit! I
tried to remember everything I did, and while it wasn't a huge amount
it was an hour of work plus testing.</p>

<p>Before I started on that path I went to the directory where IDEA
stores all of my stuff: <tt>~/.IntelliJIdea70</tt>. Under
<tt>config/shelf</tt> was a single file with the extension of
<tt>.patch</tt> and the name I'd given the shelf. Sure enough, the
tried-and-true patch format sat there, and after choosing 'Version
Control | Apply patch...' my changes were brought back in. Awesome!</p>

<p>It would have been really easy for the folks at Jetbrains to create
their own format for shelved changes, and to tightly couple the
'reintegrate shelf' functionality with the file itself, disallowing
its use anywhere else. That they didn't shows, again, how much they
know how developers work. The fact that I also could have applied them
with the command-line <tt>patch</tt> tool is also great,
and another argument for sticking with standard formats where
possible.</p>



