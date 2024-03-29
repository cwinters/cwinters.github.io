---
tags: qcon conference logistics presentation rest scala
layout: post
title: "QCon 2009: Wrapup"
---



<p>QCon was a great conference. Loads of learning, hugely smart
people. Logistically I thought everything went very smoothly,
with the exception of not having at least one or two power strips
on all the rooms. Wireless was even a piece of cake.</p>

<p>Here's a not-so-brief overview of my five days at QCon and in SF.</p>

<h2>Monday</h2>

<p>Attended 
<a href=/2009/11/16/qcon_seduced_by_scala.html">"Seduced by Scala"</a>
led by Dean Wampler. Dean is a great teacher -- very clearly
explaining some complex issues, and admitting lack of knowledge
on the one or two occasions it happened. Some might see that as
an issue (more on something similar later), but it's just reality
that we're dealing with sufficiently complicated topics and
technology that nobody will know everything.</p>

<p>And even if a teacher <strong>did</strong> know everything about a topic, it's
likely that she'd have little experience with it in the real
world. I prefer my teachers to have experience over exhaustive
knowledge.</p>

<p>I also liked that Dean seems opinionated, though not in an
obnoxious way by any stretch. More like something Dan North
mentioned in his talk on Wednesday. He called out one of the
characteristics he found in architects he admired: self-belief,
as in the courage of your convictions. </p>

<p>I like Scala, but don't yet have any experience using it in
anger. It's possible we might be able to develop a subsystem in
it, particularly if we need to take advantage of executing work
over multiple machines (using something like Akka). But we'll
see. I explicitly didn't use any IDE during the class, so I can't
say if the IDEA plugin was helpful.</p>

<p>Monday evening I got to hang out with my friend Trudy and her
fella. We hadn't seen one another in quite some time, and it was
great to catch up.</p>

<h2>Tuesday</h2>

<p>Attended "REST in Practice" with Jim Webber and Ian
Robinson. This felt a little funny because I know REST, 
<a href="http://www.cwinters.com/rest/">at least the basics</a>,
okay. But I figured these guys would have some experience using
it from an end-to-end project, and possibly guidance about
problems, objections people have and whether there are answers. I
didn't know when I signed up that they were writing a book on it
(coming out from ORA, should be great).</p>

<p>Anyway, the talk was fantastic. Even though they basically just
talked for six hours, the time flew by, and they peppered
real-world experience into their cogent and unusually clear
explanations of the standard concepts (URIs, resources,
scalability, caching, universal methods, etc.)</p>

<p>At one point during their discussion of hypermedia a light went
off for me, related to embedding hypermedia actions in your
resource. (I go on about this more in 
<a href=/2009/11/17/qcon_rest_in_practice.html">my notes</a>.) I'd always had the limitation of thinking of the
resource representation as a blob of data, but that's only part
of the picture. It may be a standard RPC-oriented way of
thinking, but it really misses one of the main points of REST.</p>

<p>I had some concerns about using this with resource actions that
might vary per user (think workflow actions on JIRA issues). But
I talked with Jim Webber on Friday after the conference was over
and he confirmed my thinking that this happens infrequently
enough that you can either just use the resource + custom actions
as-is, forgoing caching benefits, or push it down further into a
resource.</p>

<p>Anyway, if you have a chance to see them and you're at all
interested in REST, you won't be disappointed.</p>

<p>Tuesday night I wandered around a bit, then went for some sushi,
making the mistake of ordering a special off the wall that didn't
have a price. The bill was very surprising.</p>

<h2>Wednesday</h2>

<ul>
<li><a href=/2009/11/18/qcon_adventures_of_agile_architect.html">Adventures of an Agile Architect</a> </li>
<li><a href=/2009/11/18/qcon_architecture_reviews.html">Architecture Reviews</a></li>
<li><a href=/2009/11/18/qcon_continuous_deployment.html">Continuous Deployment</a></li>
<li><a href=/2009/11/18/qcon_strategic_design.html">Strategic Design</a></li>
</ul>

<p>The highlight of the day was learning about Domain Driven Design
with Eric Evans (Mr. DDD). I'll probably write more about it in
the future, but it was one of those talks that wasn't anything
earth shattering, just clicking a lot of things into place that
make a lot of sense.</p>

<p>Dan North's talk on teams and change was wonderful. One of the
bits that agile talks seem to encourage is the human interaction,
which seems sorely missing in a lot of software development
writing. Alexander Cockburn demonstrates this in the
wonderfully titled
<a href="http://alistair.cockburn.us/Characterizing+people+as+non-linear,+first-order+components+in+software+development">Characterizing people as non-linear, first-order components in software development</a>.</p>

<p>Continuous deployment was also really interesting. I mentioned to
someone going into the talk that I thought I'd come out of it
thinking that it's something you should be able to do by default,
and only not do it when you've got good and concrete reasons. It
makes a smooth deployment model possible.</p>

<p>I didn't writeup anything on the Wednesday keynote, but I liked
it. It was two VCs discussing some trends they saw, outlining
things they looked for in ventures and some trends in
opensource. They were open and funny -- it's probably a talk
they've given a number of times, but it didn't feel that way.</p>

<h2>Thursday</h2>

<ul>
<li><a href=/2009/11/19/qcon_better_architecture_management.html">Better Architecture Management Made Easy</a></li>
<li><a href=/2009/11/19/qcon_open_social.html">OpenSocial in the Enterprise</a></li>
<li><a href=/2009/11/19/qcon_architecture_for_cloud_applications.html">Software Architecture for Cloud Applications</a></li>
<li><a href=/2009/11/19/qcon_architecting_for_the_cloud_horizontal_scalability.html">Architecting for the cloud: hoizontal scalability</a></li>
<li><a href=/2009/11/19/qcon_agile_development_to_agile_operations.html">Agile Development to Agile Operations</a></li>
</ul>

<p>The first talk was by a vendor, but a technical one. People seem
allergic/hostile to these, but I think they can be great. The
demo must be given by someone who knows what they're doing, and
they need to put the product in a context and as means, not an
end.</p>

<p>The second talk, on Open Social, was also very well done. It
carved out a little space for itself and filled it nicely. I like
the model and will look into implementing it for our product --
it would be interesting to see other clinical vendors use it as
well.</p>

<p>This was the first conference where I'd seen Michael Nygard. I'm
a huge fan of <a href="http://www.amazon.com/Release-Production-Ready-Software-Pragmatic-Programmers/dp/0978739213/">Release It!</a> -- as were a lot of other people I
talked to, saying that it's "required reading" for people on
their teams. He gave a solid, clear overview of clouds and their
moving parts, pointed out some trends and injected a few
well-earned opinions. Very useful for a cloud newcomer like me.</p>

<p>The other two were also ostensibly related to clouds. I liked
Adam Wiggins: he clearly knows his stuff (he probably dreams
about it), and what they're doing at Heroku seems
spectacular. But the discussion was pretty shallow, touching on a
number of pieces without going into any in depth, or fitting them
together.</p>

<p>Stu Charlton is another guy who's clearly on top of things. His
discussion of the tensions between development and operations was
informative, and it seemed like he could talk about it for hours
if you wanted. He was a very disciplined speaker though, and
sounded like one of those folks who have given so many talks that
he had an internal clock telling him where he was in the
flow. His identification of trends where things are going to get
worse, and some ways out of it, was also great.</p>

<p>The Thursday keynote was by Don Box, and if you'd been <a href="http://twitter.com/#search?q=%23qcon">following
on twitter</a> you probably
saw quite a bit of discussion about the crash and burn. I liked
that he tried though.</p>

<p>Thursday night a college friend and his wife picked me up and we
wandered around a bit, getting some beer and dinner, before
winding up at another friend's house. More good times.</p>

<h2>Friday</h2>

<ul>
<li><a href=/2009/11/20/qcon_sustainable_design_for_agile.html">Sustainable Design for Agile</a></li>
<li><a href=/2009/11/20/qcon_language_data_and_modeling.html">Codename ''M'': Language, Data and Modeling</a></li>
<li><a href=/2009/11/20/qcon_unibet_architecture.html">unibet.com Architecture</a></li>
<li><a href=/2009/11/20/qcon_soa_at_ebay.html">SOA at eBay</a></li>
</ul>

<p>The day started off with another Eric Evans talk, and my status
as a fanboy was now complete. One of the gratifying aspects was
being able to look back at some of the things we did with
AccuNurse as really central to its success so far. I mentioned
this to Eric and he replied with the common idea behind patterns
which Dan North summed up as: if you tell me a pattern and it's
something new, it's not a pattern. I wish I'd heard about DDD
before we started development on it, but I'm glad I know about it
now, and will get the book and keep the topic in my mental
"things to follow" list from now on.</p>

<p>Don Box and former Pittsburgher Amanda Laucher presented a
Microsoft framework that allows you to create grammars and
immediately test them, then instantiate them at runtime and do
interesting stuff. It was pretty neat, and a little surprising
that this isn't more commonplace. Tom will probably see this and
mention that Haskell and other functional languages have done
this for years. :-) Anyway, it was a great talk: Don is hugely
enthusiastic (he must have said "Awesome" at least once a minute)
and knowledgable. And I liked that he did live demos of the beta
product, even if they bombed once or twice. Some people were
bitching about this on twitter, which is just mean-spirited. I
think it's great to get peeks into this stuff and where they're
headed, by someone who not only knows how they work but is aware
of their potential and can explain it well.</p>

<p>The talk on unibet.com was fascinating, but the speaker was a
typical geek one: dry sense of humor, not a lot of presentation
dynamism, and always with the assumption that the things he was
discussing were obvious. (I plead guilty to this as well.)</p>

<p>The final talk was on SOA at eBay, which was a little bit of a
departure for me. I'd avoided the SOA track (even though Ian
Robinson was giving a talk), but this seemed too interesting to
pass up. Getting technical people on the inside to talk about
their work on a site like eBay is pretty unusual. Sastry knows
the system up and down, as well as the reasons all the technical
decisions were made. He can also talk about these really, really
quickly! Their use of governance was interesting, and cleared up
some misconceptions I had about it (figuring it was just a way
to put more useless layers in a process).</p>

<p>The Friday keynote was so-so, very Oracle-centric. And again, a
lot of people really disliked it. But for me it was interesting
to see what this stuff can do, as all the dynamic cloud
provisioning stuff is new to me. It's awfully impressive when you
step back and see what's going on. That said, David Chappell is
someone who has a lot of knowledge about technology and trends
and intersections, and having him talk just about Oracle stuff as
he did seems like a waste, at least for this crowd.</p>

<h2>Talks I wish I'd been able to see</h2>

<p>Not in any particular order:</p>

<p><strong>Scaling your cache and caching at scale</strong> - Alex Miller. I love
<a href="http://tech.puredanger.com/">Alex's blog</a>, and putting this
against the scaling panel was tough.</p>

<p><strong>Java Puzzlers</strong> - Bob Lee and Josh Bloch. If only so I could
ask what they thought about the Java7 closures announcement.</p>

<p><strong>Project Voldemort</strong> - Jay Kreps. Hearing depth about one of the
distributed k-v stores would have been cool.</p>

<p><strong>Enculturating Master Craftspeople</strong> - Dave West. No idea how
this went, but it sounds fun, but not terribly useful for work.</p>

<p><strong>Clojure in the Field</strong> - Stuart Halloway. I got the Clojure
book at YAPC this year but haven't had a chance to get in. (Other
things are taking precedence.) But I'd still like to hear Stuart
talk about it; I saw him speak at a NFJS in DC about 5 years ago
and really enjoyed it.</p>

<p><strong>Designing a Scalable Twitter</strong> - Nati Shalom. Getting an idea
of how you design with something like GigaSpaces would stretch my
brain, even though Twitter-scale is insane.</p>

<p><strong>Failure comes in flavors</strong> - Michael Nygard. As I mentioned
Michael is a <strong>great</strong> speaker: engaging, knowledgable,
authoritative, but still practical. But this sounded a lot like
concrete examples from <strong>Release It!</strong>, and it was competing with
a talk by Eric Evans.</p>

<p><strong>Skeptical view of language workbenches</strong> - Glenn
Vanderburg. There were lots of positives from all the right
people on twitter.</p>

<p><strong>Building Languages with MPS</strong> - Neal Ford and Nate Schutta. I
head about this product from JetBrains a while ago but have't
really <strong>got</strong> it yet. Guess that'll wait.</p>

<p><strong>Actors, and the forgotten art of modeling concurrent systems</strong>
  - Kresten Krab Thorup. Concurrency has been on my brain, and
finding a different way to think about it would be very useful,
even if only as exercise. The one I went to instead (unibet.com)
was just okay, and I probably would have been happier here.</p>

<p><strong>Navigating the rapids: real-world lessons in adopting agile</strong> -
  Sam Newman. I heard this was "Stuff Sam will tell you at the
pub given enough beer, which sounds like fun.</p>

<h2>Other notes</h2>

<ul>
<li>Were there really two Spring Roo talks? That seems weird. I
know everybody loves Spring, but...</li>
<li>I <strong>loved</strong> the quick feedback process. They had a bin and a
stack of red, yellow, and green pieces of paper outside the
room after a talk. To give feedback you'd just pickup a piece
of paper corresponding to your mood and drop it in the
bin. Because it was so easy everyone seemed to do it, which
hopefully provided a good guide to the organizers and
speakers. </li>
<li>The food was surprisingly good, and lots of vegetarian
options. Breakfast was a little sparse, but that wasn't a big deal.</li>
<li>...the coffee was only so-so much of the time, even just
lukewarm once. In fact I think it got worse as the week
progressed.</li>
<li>The Wednesday night out at a local bar (Jillian's) was cool,
nicer than hanging in the hotel. Free beer on Friday was also
nice, and a lot of the speakers hung around for it.</li>
</ul>



