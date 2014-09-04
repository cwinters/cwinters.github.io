---
title: "Telling a story with a presentation"
layout: post
tags: techfest presentation
---

In June I gave a 30-minute presentation at Pittsburgh Techfest -- 
[slides are here](http://goo.gl/J4Tcoq) and 
[repo is here](https://github.com/cwinters/unretrofittable-201406). 
The topic changed over time and turned out a little different than I
anticipated. 

Originally this lived as a 
[poorly executed Pittsburgh Ruby lightning talk](https://docs.google.com/presentation/d/1kUqXsWpJl8lGO-_u9De-w2K0nrujuNNJnsK5mEmnz6Q/edit?usp=sharing)
whose idea I came up with day-of. It's basically a listicle of things
you should try to think about when a project starts because they're hard
to undo (or redo) later.

The origin of the idea came from my experiences at AccuNurse with
a Java application. And a few months after leaving there I looked back
with some fresh eyes and jotted down a list of things I wish we'd done.
That list is pretty much the same as the one from the lightning talk, but
some of them don't fit quite as well with the Ruby community -- serialization,
for example, is much easier.

The talk was poorly executed because I only got through half the items, and
even those I got through were a muddy mess. (That's what I get for coming up
with the talk that day...) Still, the ideas seemed useful and I proposed a 
talk on the same topic for Techfest which got accepted.

## Preparing by writing

Instead of my usual preparation -- which is to write an outline, translate that
into slides and then go over the slides too-few times (1) -- I decided to write
a story. (You can see big chunks of it in 
[the notes](https://github.com/cwinters/unretrofittable-201406/blob/master/notes.md)) 

And in the course of writing the story the presentation changed. Instead
of a listicle I wound up with a theme that carried through just a few items. 
The process of writing in paragraphs put me in more of a storytelling mindset
than an information shotgunning one. These are the types of presentations that
really resonate with me (any of 
[Dan North's](http://www.infoq.com/author/Dan-North) are a good example), 
I just never thought about the process enough to do it myself.

The story -- well, more of a theme -- I settled on is one Anthony picked up on
during the talk:

<blockquote class="twitter-tweet" lang="en"><p>.<a href="https://twitter.com/cwinters">@cwinters</a> is giving a subtalk about event sourcing <a href="https://twitter.com/hashtag/pghtechfest?src=hash">#pghtechfest</a></p>&mdash; Anthony Mastrean (@anthonymastrean) <a href="https://twitter.com/anthonymastrean/status/475289485446746112">June 7, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

More broadly, I wanted to stress the idea that if you thing-ify user actions
you get a lot of really interesting side-effects. REST-land sometimes talks
about resource-ifying processes so you can manipulate them using 
the uniform interface. I gave an example of "Nouning Transactions" in this 
[now-ancient presentation](http://www.slideshare.net/cwinters70/introduction-to-rest-and-jersey)
(slide 47) that gives the idea.

Anyway, while I'm unsure how the presentation went itself (it wasn't recorded),
I'm pretty happy with the process and will try to keep doing that for future
presentations.

----
(1) The one exception to this routine was when I did a presentation with
[Carol](http://twitter.com/carols10cents) at last year's Techfest, 
which was a great experience in multiple ways that I'll talk about later.


