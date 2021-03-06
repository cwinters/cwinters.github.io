---
tags: pittsburgh conference techfest rest scala distributed
layout: post
title: "Impressions of Pittsburgh TechFest"
---



<p>Saturday saw Pittsburgh's first 
<a href="http://pghtechfest.com/">TechFest</a>, a day-long set of
sessions with seven (!) tracks covering a number of different
technologies and disciplines. I wound up getting there about 15
minutes after lunch ended[1] and ran into a former co-worker, and
instead of going to the current session we chatted. Despite the
environment (school halls aren't the best place for a hallway
track) that's probably the best reason to attend an event like
this. Sure, you learn things here and there -- and some of the
sessions were long enough to get meaty -- but having a bunch of
motivated people around each other is the real payoff.</p>

<p>The two sessions I did see appeared to be pretty different but
wound up being quite similar in scope. The first was on <b>Scala
and Actors</b> from <a href="http://twitter.com/jsuereth">Josh
Suereth</a>. Josh is both super nice and super smart, but that's
not always a great combination for a presentation. The last time
I saw him speak was in October 2010 for an overview of Scala,
which (referring back to my notes) was jam packed with
information but unfocused, which is a problem with a lot of
technical presentations, including my own.</p>

<p>This was much different. Josh started by demoing in a shell
the amount of Scala you needed to know for the presentation, and
then moved on. It's so easy to get wrapped up in language intro
because it's easy and I'm sure he could riff on Scala nuts and
bolts for hours. But while it would be easier for Josh -- no
preparation needed! -- that's not going to be as useful for
the audience.</p>

<p>The main point of the talk was to discuss actors and some ways
that they shape your solutions, to get you thinking in actors and
appreciate some core differences as to how they'd shape design. A
key point he mentioned multiple times is that you need to think
<b>topologically</b>, not lexically (when thinking of error
handling) or even in objects. To show what that meant he took a
real-world problem (document indexing and searching with <a
href="http://www.eaipatterns.com/BroadcastAggregate.html">scatter-gather</a>)
and broke the system down into the important components, pointing
out trade-offs and the reasons for doing things like creating
temporary actors to hold the state (because the aggregating actor
can only process a message at a time, you don't want it to
wait).</p>

<p>He went pretty quickly through the material, but he covered a
useful patch of ground in enough depth to provide lots of grist
for your mill. And he also left enough time at the end to answer
some substantive questions, even referncing deep detail
(interaction with the Java memory model) about the Akka
implementation of actors in response to a question about whether
they could be ported to the CLR. It was exactly what I was hoping
for.</p>

<p>The second talk I went to was on <b>Hypermedia APIs</b> from
<a href="https://twitter.com/#!/steveklabnik">Steve
Klabnik</a>. I probably shouldn't have gone because (a) <a
href="http://www.cwinters.com/rest/">I've talked on this
myself</a>, and (b) pretty much knew what to expect from Steve. I
also figured I'd agree with everything he said. (Which I
did.)</p>

<p>But it was still very much a worthwhile talk. Steve knows this
material backwards and forwards, and needed no notes to talk
cogently and in depth about subjects as varied as his "favorite"
RFCs, history of REST and its back-and-forth in the internet
arena, and post-structuralism as it applies to decentralized
networks of data and people. And while he referenced that it's
hard to talk about REST without using its terms, he was able to
explain things to newcomers clearly and concisely. The talk was
an hour and a half, but it certainly didn't feel that way.</p>

<p>A couple thoughts I had during the talk:</p>

<ul>

  <li>It would be interesting to see a concrete example of a
  media type that could be interpreted different ways depending
  on its definition. (For example a 'screens' attribute in a
  media type describing a film's distribution vs 'screens' in a
  TSA report.)  But, as he said, this is also as much art as it
  is science and to be done well would probably be another many
  minute talk. Which I look forward to hearing from Steve.</li>

  <li>He referenced that we keep repeating the mistakes of
  distributed objects. Another great talk (which might go along
  with <a
  href="http://www.infoq.com/presentations/vinoski-rest-serendipity">this
  presentation from Steve Vinoski</a>) might go over <b>why</b>
  we keep doing so. Why do we keep repeating this? Is it because
  of the never-ending tension between management who wants
  interchangeable programmers and repeatable processes (e.g.,
  creating clients through code generation) rather than
  craftspeople? (Simplistic, but still.)</li>

  <li>Hashing over media types winds up being a lot of the work
  done by domain experts so they can talk to each other, or
  create systems that talk to each other. Think HL7 or any of the
  X12 domains. It's incredibly hard work for non-trivial domains
  to get people to talk and understand one another, much harder
  to get computers to understand one another as well.</li>

</ul>

<p>So a short, but great day. Looking forward to the next
one.</p>

<hr noshade="noshade" />

<p>[1] In addition to hanging out with Ella, the entry to Laroche
is marked quite sparsely and I drove past it once. Seriously.</p>



