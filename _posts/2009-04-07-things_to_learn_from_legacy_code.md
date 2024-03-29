---
tags: legacy programming learning
layout: post
title: "Things to learn from legacy code"
---



<p>Recently I listened to <a
href="http://itc.conversationsnetwork.org/shows/detail3987.html">a
presentation by DHH</a> from September 2008 on what "legacy"
code means.[1] His argument is that legacy isn't an attribute of the
code, it's an attribute of the person looking at the
code. Further, what you're working on <strong>right now</strong>
is legacy code to someone in the future. Depending on your
knowledge of the platform that someone could be you two weeks
from now.[2] Or it could be your new team member three years from
now.</p>

<p>A couple other things worth noting from the presentation:</p>

<p>1. I thought very interesting his assertion that the better
  you get at what you're doing, the longer it takes for you to
  recognize your code as legacy. This isn't because you have
  blinders on, just that you've internalized a sufficient amount
  of the platform, patterns and idioms that you're not changing
  as rapidly, that you're doing more things right the first
  time. It also means that to get the same 'jumps' in learning
  you'll be working on projects for a longer time and getting
  into unsexy 'maintenance', which is underappreciated as a
  learning area IMO.</p>

<p>2. His honesty at looking back at his own code and
  reasoning. It can be tough to say that things you've written
  stink -- and even tougher to do so in front of an audience! --
  but IMO it's a necessary part of growing. Part of this is
  removing intent from the equation: you have to trust that
  decisions you made at the time were appropriate given your
  constraints (budget, time, technology), problemspace, and your
  understanding of all these. Intervening time can change
  everything, so don't beat yourself up for doing stupid
  things. Recognize it and move on.</p>

<p>In a <a href="http://www.infoq.com/presentations/vinoski-rest-serendipity">recent
presentation</a> Steve Vinoski referred to "legacy software" as
"software that works". And, to carry forward a point above,
legacy software codifies the decisions made based on the
organizational knowledge and pressures existing at the time it
was planned and written. You might not agree with the decisions,
but you need to respect them, because they represent the best
efforts of your colleagues and peers. And they're not as stupid
as you think.</p>

<p>It's easy for us to look at a system and point out all its
flaws. (I've been embarrassingly guilty of this in the past.) But
without knowing <strong>why</strong> things were done you're in
danger of making the same mistakes, just using a different
technology or perhaps at a different architecture layer.</p>

<p>For instance, how <a href="http://healthcare.vocollect.com/">our 
system</a> represents the nursing assistant plan of care differs
radically from that found in the previous version. The plan of
care is fairly large (~500 or so items) and when we translated
each item from the earlier version we discussed its clinical
intent, its effects elsewhere in the system (print reports,
documentation to the government, etc.), and whether it was doing
its job as intended. We tossed some items that were too specific
(e.g., tied to a single customer's process) or unused, added some
that weren't covered, and adapted others to be more flexible. But
we only did so after at least trying to understand what the
original was doing. It took a long time, but it had the
beneficial side-effect of getting us familiar with the domain as
well as the types of decisions made in it.</p>

<p>For all these changes the external representation to the Nurse is
pretty similar. Nurses have a pretty static notion of what such a
plan of care looks like and should include, and how it's broken
down into sections ('Bathing', 'Meals', etc.). After reviewing
all the old items in the plan of care we created a set of
subsections ('Cautions', 'Monitoring', 'Special Equipment', etc.)
to make sense of the hodgepodge found in the earlier version, and
then applied them uniformly to all the different sections. So we
made them learn something new, but they generally only needed to
learn it once. And people using the system for the first time
would have a simple way to locate something on a care plan. We
made these decisions with a domain expert and, for the most part,
they've held up.</p>

<p>My last idea for now about legacy software is a general
irritation. I'd guess that most people writing software today are
maintaining or adapting existing systems. Creating new software
is sexy and gets lots of press, but that's not where most people
are working.</p>

<p>But it seems that most software frameworks are optimized for
those creating new systems.[3] I can understand the need to have
your 'quick start' tutorial create a new system and start using
it because of space constraints -- you need it to be quick! But
frameworks rarely discuss what to do when you want to use it with
an existing system -- no, I don't want your framework to create
my schemas; no, I can't use an artificial primary key because my
table already has its own; no, I can't intuit the relationships
from table names because I actually have foreign keys in my
system.</p>

<p>The main reason projects don't do this is likely that existing
domains are too complicated to deal with in documentation --
plus, who likes writing documentation? And I'm sympathetic to
that. But I think frameworks are missing a great opportunity to
lower the barrier for most of the software development population
who might be interested in a framework but have trouble getting
started because of the emphasis on greenfield systems.</p>

<hr noshade="noshade" />

<p>[1] Since getting the G1 (and exercising a few times a week)
I've been listening to a lot more podcasts, and one of the feeds
I'm catching up with is 
<a href="http://itc.conversationsnetwork.org/">IT
Conversations</a>.  So it's taking a while to get up to 'current'
-- it might not be new to you, but it is to me.</p>

<p>[2] ...and your knowledge of the domain, which is something I
want to write more about.</p>

<p>[3] I could be wrong about this. I've been heads-down for
quite a long time, so my ideas may be out of date. Like
everything else about me.</p> 



