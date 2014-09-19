---
title: "Some 'Superpowers' I've seen, part 1"
layout: post
tags: behavior practice documentation organization collaboration
---

In August I said:

<blockquote class="twitter-tweet" lang="en"><p>Talking with my wife about <a href="https://twitter.com/SteelCityRuby">@SteelCityRuby</a> lightning talk, she said: &quot;Why not talk about the problem you&#39;re working on?&quot; She is so smart.</p>&mdash; Chris Winters (@cwinters) <a href="https://twitter.com/cwinters/status/499738747945361408">August 14, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

...and then didn't do a lightning talk. The talk Barb convinced me to do wound
up being too complicated to try and come up with in a short time -- versioning
your APIs. And I thought the original talk was too self-serving so I skipped it.
Which I think was the right call -- it wouldn't have fit well with the other
lightning talks, which were excellent.

But, since this blog is **entirely self-serving** I have no qualms about
talking about it here.

The main idea behind the lightning talk: I'm old, and over that very long
period of time have noticed some behaviors that can set you apart from your
peers. Some of them are things I do, some of them I've seen others do. I called
this your "secret sauce," after one of my former bosses used this phrase in a
one-on-one that really opened my eyes about how I should be thinking about my
career. (Maybe more on that later.)

None of the behaviors is anything novel. Few things are. (That's something else
old people say, sorry.) I'll go through them one-by-one and spend way more than
a lightning talk on each.

## First up, documentation

Seriously!

One generic but powerful way to distinguish yourself among peers is to do
things that:

1. everybody recognizes should be done, but 
2. nobody likes to do.

I think few people would argue that documentation doesn't meet those
requirements. And I'm not even talking about creating old-school reams of
Framemaker documentation -- that's the sort of thing that gets out of date
quickly and never updated. 

Documentation in its best form gives you broad ideas of how things fit
together, and it tells you why it is the way it is. It's possible to get the
former by reading code, though much slower, but not the latter. Yet the **why**
of a feature or approach or architecture can be far more illuminating than the
how.

Granted, documenting systems is a big job. But why not start small and make
things better incrementally? Some examples:

* Your project's README. It doesn't have to be exhaustive, but it's probably the
  first thing people new to the project read, and it should get them started
  practically (environment etc.) but also thematically (what we are 
  actually doing, common patterns, areas of complexity).
* What are the things that everyone forgets because they're only done
  every few months? The ones where you have to hunt down some magic incantation
  that got posted to HipChat that one time.  Figure out where the hard parts
  are -- normally they're the inscrutable error messages you get along the way --
  and add guidance about the concrete steps that will make things right.
  (Toot-my-own-horn example at end.)
* What hurts? Every project of a decent size has subjects that people
  dread working with. Sometimes it's because they're poorly designed
  and brittle. But sometimes it's because the domain is complicated,
  and if you don't understand the domain you'll never understand why
  the code is like it is. So help everyone understand the domain!
* Find common patterns of use that the team wants to encourage and pull them
  up into a document. These might be in package-level documentation,
  or a FAQ, or something like that. But IME the thing that gets people to 
  click with something is seeing a fleshed out example.

## Leveling up: development vs documentation spikes

As you get better at this you might find that you start thinking about problems
in terms of documentation, or how to more clearly spread the knowledge about
what you're doing. 

I think working with problems in this way can result in you exerting some
interesting influence, because:

> People who write documentation can define the terms of the conversation.

For example, say your team has decided to rewrite a substantial subsystem
because it's too brittle and there are a number of changes in the backlog that
everyone agrees will take too long for the business. What are some different
ways to decide on the approach to take?

- brainstorm for ideas and then choose based on another approach
- discuss and reach consensus
- loudest voice wins
- top-down dictatorial
- "do what we've done before"

Any of these may be appropriate in your situation. But IME people rarely speak
up about what to do beyond handwavy ideas. This may be because they don't
actually know what to do, or maybe they're 
[scared of proceeding](http://www.infoq.com/presentations/Embracing-Uncertainty)
without knowing what's going to happen. (Which probably means they're in an
environment that punishes ideas, but that's another post.)

One way to make the handwavy ideas more concrete through a 
[spike](https://www.scrumalliance.org/community/articles/2013/march/spikes-and-the-effort-to-grief-ratio).
I think true development spikes are a great way to do this. Some potential
problems:

1. How many times have you seen a spike become the implementation?
2. Despite their intended purpose spikes often tend toward technology exercises
   ("I want to play with the new shiny!")
3. A working spike can cease conversation in ways you might not like.

The first is both endemic and regrettable, and the second is probably 
a whole other post. (Again!) But I want to talk more about the third. 

The development spike and documentation spike (for lack of a better term) have
a great deal in common. Both are trying to make abstract ideas and 
trade-offs more concrete by plumbing an idea through some semblance of reality.
The development spike does this by implementing as little as possible to prove
the idea right or wrong. The documentation spike does this by both describing
and creating examples of how data flows among components and highlighting
problems along the way.

Both the development spike and documentation spike take advantage of
[first-mover advantage](http://en.wikipedia.org/wiki/First-mover_advantage).
It seems like nearly every human endeavor has such a thing -- people
give a greater weight to things they see first. It feels weird to me to think
of technical decisions in what is often used as a smarmy marketing term. But
the marketing people study psychology, or at least they read summaries of
people who study it, and I think it's an apt comparison.

Both types of spikes can also be a form of 
[working backward](http://www.allthingsdistributed.com/2006/11/working_backwards.html) (1), 
though I think it's more explicit in documentation than development. Vogels's
examples -- press release, FAQ, user manual written as if the product were
complete and released -- force you to focus on the benefits, what you're
actually trying to achieve, rather than the fun day-to-day work.

But I think where documentation has an advantage is that you can weave intent
into the narrative and augment it with examples in the same flow. Even if
development spikes include such discussions
([ha!](https://www.youtube.com/watch?v=t7Tm0SQT7N4)) they'll be a separate thing.

I think it's also better because you're not constrained by implementation. You
might see this as a weakness, something similar to product managers creating
features that are entirely detached from reality. But I find if I'm not constrained
by writing about particular features of implementation I'm freer to focus on 
[one level of the cognitive domain](http://en.wikipedia.org/wiki/Bloom's_taxonomy) 
rather than bouncing between levels. I'll still have the big-picture implementation 
details informing my writing, but it's passive based on internalized experience 
rather than a direct idea under discussion. Which just means I won't write
documentation assuming that network calls are free, processes aren't I/O bound,
etc. It's a little dangerous, but if you've grown to use your intuition well
you've probably already evolved your own set of checks and balances.

Finally, there's a feature that comes from the fact that nobody likes
to write documentation: you may get a bigger influence on the final outcome
than you would if you wrote code. 

This may also sneaky, but you're not tricking people! You're doing everything
out in the open. And in fact because many things you're doing are more
accessible to non-developers, you'll need to be prepared for more input and
criticism, including from people who may be better writers than you. 

## The gift that keeps on giving

Want anecdote-as-proof? Internet and Pittsburgh superstar Carol Nichols said
this to me, nine months after I left the project:

<blockquote class="twitter-tweet" lang="en"><p><a href="https://twitter.com/cwinters">@cwinters</a> every time 
i have to ssh to a new server with ttmscalr, i am thankful for the amazingly helpful 
instructions you wrote &lt;3 :)</p>&mdash; Carol (@Carols10cents) <a href="https://twitter.com/Carols10cents/status/508242232429019136">September 6, 2014</a></blockquote>

----

(1) "Working backwards" is an idea I hope to discuss later because I think it's
a powerful way to get yourself out of a rut. It's probably already got loads of
posts and books written about it already, but what's another $0.02 on the 
internet going to hurt? It's in 
[the hopper](https://github.com/cwinters/cwinters.github.io/blob/master/ideas.md).
