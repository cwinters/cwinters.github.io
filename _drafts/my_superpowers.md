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

The main idea was: I'm old, and have some behaviors I've noticed that can set
you apart from your peers. Some of them are things I do, some of them I've seen
others do. I called this your "secret sauce," after one of my former bosses
used this phrase in a one-on-one that really opened my eyes about how I should
be thinking about my career. (Maybe more on that later.)

None of the behaviors is anything novel; few things are. I'll go through them 
one-by-one and spend way more than a lightning talk on each.

## First up, documentation

Seriously!

One generic way to distinguish yourself is to do things that:

1. everybody recognizes should be done, but 
2. nobody likes to do.

I think few people would argue that documentation doesn't meet those
requirements. And I'm not even talking about creating old-school reams of
Framemaker documentation -- that's the sort of thing that gets out of date
quickly and never updated. 

Why not start smaller? Some examples:

* Your project's README. It doesn't have to be exhaustive, but it's probably the
  first thing people new to the project read, and it should get them started
  practically (environment etc.) but also thematically (what we are 
  actually doing, common patterns, areas of complexity).
* What are the things that everyone forgets because they're only done
  every few months, and then they have to hunt down some HipChat post 
  with a magic incantation? Figure out where the error happens and replace 
  that inscrutable error message with step-by-step instructions on 
  how to fix it. (Example at end.)
* What hurts? Every project of a decent size has subjects that people
  dread working with. Sometimes it's because they're poorly designed
  and brittle. But sometimes it's because the domain is complicated,
  and if you don't understand the domain you'll never understand why
  the code is like it is. So help everyone understand the domain!
* Find common patterns of use that the team wants to encourage and pull them
  up into a document. These might be in package-level documentation,
  or a FAQ, or something like that. But IME the thing that gets people to 
  click with something is seeing a fleshed out example.

### Leveling up

As you get better at this you might find that you start thinking about problems
in terms of documentation. (This is a form of 
[working backwards](http://www.allthingsdistributed.com/2006/11/working_backwards.html) 
that I have in the blog post hopper.)

 This is when you can start exerting some interesting
influence, because:

> People who write documentation can define the terms of the conversation.

For example, say your team is thinking about rewriting a substantial subsystem.
What are some different ways to decide on the approach to take?

- brainstorm
- discuss and consensus
- loudest voice
- top-down dictatorial
- "do what we've done before"

documentation can make hand wavy more concrete -- lots of examples, discussion
of intent and trade-offs 

process of plumbing through some of your ideas and getting them to meet reality

relationship to working backward

- It seems like nearly every human endeavor has a significant 
[first-mover advantage](http://en.wikipedia.org/wiki/First-mover_advantage) -- people
give a greater weight to things they see first. It's weird to think of 
technological decisions in smarmy marketing terms. But the marketing people study
psychology (or at least they read summaries of people who study it)

Additionally, there's a feature that comes from the fact that nobody likes
to write documentation: you'll get a bigger influence on the final outcome
than you would if you wrote code. And you're not tricking people! You're
actually giving everyone a fighting chance to make their wishes known...

### Gift that keeps on giving

Want proof? Superstar Carol Nichols said this to me, nine months after I left the project:

<blockquote class="twitter-tweet" lang="en"><p><a href="https://twitter.com/cwinters">@cwinters</a> every time 
i have to ssh to a new server with ttmscalr, i am thankful for the amazingly helpful 
instructions you wrote &lt;3 :)</p>&mdash; Carol (@Carols10cents) <a href="https://twitter.com/Carols10cents/status/508242232429019136">September 6, 2014</a></blockquote>

