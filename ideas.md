## Working backwards

[Werner Vogels](http://www.allthingsdistributed.com/2006/11/working_backwards.html)

Reference in special sauce #1

## Presentation with someone else

- Caveat: sample size one, with one being awesome Carol

- Preparation better because you don't want to let someone else down

- Presenting better because you get a break

## 2014-08-13 Some secret sauce

(bad title, change)

Some of these I do, some of these I've had the fortune of working with amazing
people who did them seemingly without thinking.

1. Unexpected gift at an unexpected time. 

In development one translation is "documentation that's there when I need it"

Documentation:

- RDD: Readme driven development
- Explain why - large AND small scale (take care of the "oh, there has to be a
  better way of doing this" that has actually already been tried!)
- Maintain README and setup
- What hurts, and why?

2. Learn how your database works.

Time spent optimizing your database interactions will pay off 10x (or more)
than time spent optimizing your code. This also means you need to learn how to
listen to what your database is telling you -- monitoring, statistics
gathering, logging, etc.

A nice thing about this: it doesn't change as often as other aspects of our
world. And some of the things you learn -- like about column ordering in
indexes -- are often applicable across vendors.

3. "We are what we pretend to be, so we must be careful about what we pretend to be."

If you want the benefits of collaboration, then collaborate. You can't turn it on
just when you want to do it, it has to bee a habit. So when you work in a corner off 
by yourself and people say you're building a silo, listen. Even if you do lots of
good documentation.

Conway's Law and its implications.

4. "No matter what they tell you it's always a people problem" (and some more
random wisdom from Jerry Weinberg)

Learn to let things go. You don't have to win every battle -- and even thinking
about them as battles puts you in a bad place to start with. Software development
is not a zero sum game.

5. Have something to mediate the firehose of the world.

Software development is one of the best jobs in the world. We're not in
physical danger, the pay is generally pretty great, there's opportunity for
anyone to learn(1) on their own vs going through an expensive multiyear education
gateway. And on top of all that you get to __make stuff__. 

(1) Totally not the same opportunity for everyone -- disparaties in education, 
financial means, stress related to life circumstances, etc. May want to
rephrase... idea is to contrast with law, medicine, even physical engineering
which require a more formal process that requires $$ and time.

But one of the tradeoffs for all this is that you have to keep up. And that's
really hard, because it changes all the time. Twitter, RSS, meetups =>
increasing cycle time.

6. Work up the stack.

Previously this was pitched to developers to ensure they wouldn't get replaced
by overseas resources: if the work you do is a commodity then don't be
surprised when it's treated that way.

But I think it's better pitched as a positive: if you know what you're building,
why you're building it, and how it will be used then you'll build a better thing.

## Thinking about your career

- Logan one-on-one where he talked frankly about what makes him different

- What makes you special? How do you cultivate that?

- Nobody cares about your career but you. You are not a special snowflake.

- Smallest unit of failure in a company is the team. (Find tweet in my stream
  from ~Sep 6-7 with presentation image)

## What if you're not who you think you are?

I've taken the <a href="http://en.wikipedia.org/wiki/Myers-Briggs_Type_Indicator">MBTI</a>
since 1989 or so, and every time I've been an
<a href="http://en.wikipedia.org/wiki/Intp">INTP</a> (like a
lot of software developers). In particular, the 'I' portion of
that has been a solid part of my identity for as long as I can
remember, in particular the last part of the E vs I list from the
wikipedia page:

- Extraverts recharge and get their energy from spending
  time _with people_, while introverts recharge and get their
  energy from spending time _alone_.

I've always taken this as a given, because it's absolutely true
that I don't like meeting large groups of new people, or making
small talk with bare acquaintances. Those are things salespeople
are good at, or jocks, or geniuses, right?

But what if instead of being an absolute it was a conditional?
That is, what if I just wasn't spending time with the *right*
people? Or what if I simply wasn't paying attention to the times
where I *was* recharged with the right people because, well,
that's just not me?

This is probably just navel-gazing bullshit, but I think I'll
stick with it for a while. (I keep thinking of Jude Law echoing
to himself over and over in "I Heart Huckabees": "How am I not
myself?") Not only is the whole idea disturbing, but some
implications are as well (what opportunities have I missed? who
the hell is 'me'?). But that's okay. It's better to admit fault,
figure out what's going on, fix it and move forward, honestly and
transparently. Or at least try.


## 2010-06-22 Blog idea: Wall off complex functionality

Many times when implementing a feature about 80+% of its 'guts'
will be straightforward with no contention. By 'guts' I mean what
we frequently call 'business rules' -- orders placed, inventory
changed, contracts approved, whatever. And by 'straightforward' I
mean the business rules are well defined and understood, and both
the ways in which user manipulates the rules and the data fed
from and resulting from the rules are nicely constrained.

If everything were like that the job wouldn't be so
interesting....

Wall off complex functionality  -- example of determining whether
a skin condition was present on admission; first stab at defining
interface [isPresent...( SkinCondition )] was OK, but going ahead
and *using* that interface showed that passing in a target time
was a crucial piece of required context. Once everything works
and we know that the inputs and outputs are defined and correct
we can go ahead and implement.

## Stress

"I think it’s a crock. I think stress is what intelligent people
do when they cannot control the world."
(http://blog.penelopetrunk.com/2010/07/13/the-farmer-reviews-three-business-books/)

So just let go.

## Some HL7 impressions

I've spent the last four days in Phoenix for an HL7 working group
meeting. It's a thrice-yearly meeting where several hundred
people get together, face to face, and have meetings to hash out
issues that have come up about healthcare messaging. While I'm
not yet up to speed on everything to directly participate, my
work thought it useful enough to sponge up information and see
how the sausage gets made.

Short answer: useful, and very illuminating.

I wound up sitting in on two primary groups:
<a href="http://wiki.hl7.org/index.php?title=Patient_Care_WG">Patient Care</a> and
<a
href="http://wiki.hl7.org/index.php?title=Structured_Documents">Structured Documents</a>.
The latter

Some of the tensions I think I observed in my time:

(first two: "perfect is the enemy of the good")

- Model is central (or "I never met an abstraction I didn't like")
- Architecture must be correct.
- Tools will solve our problems.
- Specific vs generic
- "Just add a transform"

## What an amazing time (HTTP + what it enables)

For each of these, go into detail about the link + HTTP
transactions + what's going on behind the scenes (querying an
inventory tracking system, etc.), then the
kicker:

Time for this whole transaction from start to finish: about 75
seconds (including the 20 seconds 'waiting' for my cellphone to
get the email).

1. Go on website and find paperback book of poetry that Barb
wanted for her birthday.
2. Add it to my virtual 'cart'
3. 'Check out', providing an email and password
so I can be identified
4. Confirm my shipping address and credit card, placing the order
5. 20 seconds later, my cellphone chirps letting me know of a
confirmation email about that order

## Learning new domain + new technology + new architecture

...probably not a good idea. Part of designing an architecture is
fit for purpose. Do you need to optimize for a rapidly changing
domain, or for straightforward feature consistency? (In my mind
they tend to be ends of a continuum -- being adaptable to change
means more abstraction, which means less straightforwardness.)

- learning domain: you don't know where/how it will change; you
  don't know where to concentrate the abstractions

## Movie: Little Children

Last night Barb and I watched <a
href="http://www.imdb.com/title/tt0404203/">Little
Children</a>. I liked it, but it felt oddly flat, and not just
because it was a film about repressed suburbanites.

- book adaptation: author best person to adapt?
- sara's husband: where was he? did he actually serve a
  purpose besides making winslet's adultery more acceptable? how
  is it even possible she'd be married to this guy?
- parents (sara and brad) seemed to be helicoptering a lot;
  attempts to assuage guilt at being disconnected?
- men portrayal: shallow, nostalgic (Rabbit from Updike); Brad
  couldn't even lie well when kathy asked him about "aaron's new
  friend"
- nice casting: sara's daughter (lucy) looked a *lot* like her
- Barb being more critical of movies, me consumer of narrative

## Motivation

My new policy: I'm no longer going to question your motives. I'm
going to take what you tell me at face value. So if you say
you're worried that the Obama administration is going to turn the
country socialist, I'm not going to assume you're a paranoid
nut. I'll ask, "How will that happen?" or "What do you think a
socialist country looks like?" to try and get at the root of your
worry.

I do believe that most people are good. I also believe that hate,
anger, and mistrust are easy when facing something as large as a
corporation, or the government, or a religion. But people
comprise that religion, individuals.

## Reversing disintermediation

- So many aspects of our life are so complicated. Common practice
  is to have someone else deal with that complication. That can
  work, but only if that person knows you and doesn't have
  competing interests that outweigh the personal
  relationship. (Example: our benefits person at Vocollect.) But
  if you work for a large company the equiv doesn't know you, and
  will make decisions about you that she doesn't know even affect
  you.

  Alternatively, our practice has been to just let "someone else"
  take care of it. Tim O'Reilly quotes someone referencing our
  view of "Vending machine government" -- I put in taxes, I get
  out services. In that view the only control we have is taxes,
  so that's what people complain about. What's the alternative?
  Getting involved in politics? Is it?

  Insurance (esp health), buying a car, buying a house, financial
  planning. All areas where the internet is supposed to help us
  disintermediate, take control. Problems are: (1) there are so
  many hours in the day; (2) we lose the strength of our
  voice. An insurance company is fine to trample all over you and
  your family, leaving you broke and sick without a second
  thought. So willing to trample over you if they know your
  broker is responsible for 500 other families?

  Rise (rebirth?) of the personal broker?

## Eventually I will need to focus

Even though I never put this out (originally from ~2009/10), revisit with
experience?

For my career I've been more in the 'jack of all trades' camp
than the 'master of one'. This has served me well so far...

- older programmers as generalists? I don't think so, but...
- too much information! (recent REST presentation)
- areas for focus:
  -- healthcare standards and messaging
  -- system design and implementation
  -- getting team infrastructure up and running (build systems,
     continuous integration, source control, automated testing)

