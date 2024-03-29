---
tags: qcon conference design domain requirements iterative
layout: post
title: "QCon 2009: Sustainable Design for Agile"
---



<p>(or "Quick and Sustainable Development of Complex Software")</p>

<p><strong>Eric Evans</strong></p>

<p>"We should do a nice design, but we just don't have the time"</p>

<ul>
<li>Indicates the value you place, you'd never hear "We'd like to
make money, but we just don't have the time."
<ul>
<li>"Modeling and design take extra time, but they pay off in
the the long run" (<strong>excuse</strong>)</li>
</ul></li>
</ul>

<p>What is your goal?</p>

<ul>
<li>Implement user story? Design <strong>will</strong> slow this down (this is
where agile focuses)</li>
<li>Complete releasable set of stories with acceptable bugs? (here,
modeling and design pay off)</li>
<li>Deliver release that can be extended to next one? (modeling and
design pay off here, big time)</li>
<li>Deliver a clear and cohesive user experience? (again, pay off
big time); being too feature driven can undermine this</li>
<li>Deliver something that advances the business strategy?
(choosing features is more <strong>tactical</strong>)</li>
</ul>

<p>Design advocates have a lot to answer for, lot of failures</p>

<p>XP: "No BDUF, YAGNI, we'll refactor"</p>

<ul>
<li>EE involved in such projects: there <strong>was</strong> design going
on, along with refusal to accept sloppy code</li>
<li>"Do the simplest thing that could possibly work" misinterpreted
as "quickest" but "simplest" actually implies a lot of work</li>
</ul>

<p>Terms:</p>

<ul>
<li>domain: sphere of knowledge or activity</li>
<li>model: system of abstractions; we typically think of UML,
but... it's a visual representation of a program
<ul>
<li>distilled form of domain knowledge, rules, assumptions and
choices</li>
</ul></li>
</ul>

<p>When are models useful?</p>

<ul>
<li>when complexity of project in understanding and communicating
about domain; not simple CRUD...</li>
<li>being selective of modeling work is critical</li>
</ul>

<p>Why modeling has not advanced, misconceptions</p>

<ul>
<li>Myth: Drive design from model ==> upfront analysis; WRONG: time
you know the <strong>least</strong> about a project is in the beginning;
upfront analysis is a way of locking in your ignorance</li>
</ul>

<p>DDD + Agile</p>

<ul>
<li>Technical solutions can distract us</li>
<li>Feature-orientation can fragment model</li>
<li><p>Up front analysis locks in ignorance</p>

<ul>
<li>So iterations <strong>feed understanding</strong> into projects</li>
</ul></li>
<li><p>Myth: Need tools that let us express models without getting bogged
down in detail => need tools that allow less skilled developers
to use parts created by smarties; WRONG: developers need to
<strong>leverage</strong> design, not use it to replace thinking</p></li>
<li><p>Myth: Need tools to raise level of abstraction from programming
=> visual programming, UML extensions; WRONG: language is our
fundamental abstraction tool, including when we create model;
language starts with <strong>talking</strong>, fits great with Agile; every
time you talk to your customer you're learning the domain</p></li>
</ul>

<p>Favorite modeling tools:</p>

<ul>
<li>Whiteboard</li>
<li>xUnit: intent to express domain in code (not necessarily
executable)</li>
<li>Mouths and ears</li>
</ul>

<p>(video: s/w expert and domain expert collaborate)</p>

<p>Domain expert is changing the software expert's view of the
domain and model, changing an assumption as to when the state can
be realized (balance of acct vs balance according to contract).</p>

<p>DDD can be undramatic</p>

<ul>
<li>Walking through concrete reference scenario (users like
focusing on these)</li>
<li>Creative collaboration</li>
<li>Refinement of ubiquitous language and therefore model</li>
</ul>

<p>Another video with software driven process (vs customer), feature
driven</p>

<ul>
<li>What's a "special case"?</li>
<li>"Special case" means our model doesn't accommodate; too many of
these means we need to adjust</li>
<li>software-focused modeling, agile => focused on green bar! just
get the feature working</li>
<li>(from video) "I <strong>guess</strong> you'd get the right answer that way"
<ul>
<li>red flag that user doesn't agree with model, or doesn't
understand </li>
</ul></li>
<li>On projects when there's dissonance we say "We'll fix that
later", but we never do
<ul>
<li>Example of video with "dummy payment" or "fake principal"
because our assumption is that someting <strong>MUST</strong> exist in a
particular place</li>
</ul></li>
</ul>

<p>"If we must have violent water-based metaphors, I do a whirlpool
rather than a waterfall."</p>

<p>(Domain Language Model Exploration Process -- diagram and
explanation from draft of paper.)</p>

<p>A few highlights from this:</p>

<ul>
<li>tell stories, then explore; some users are better about this
than others, but they'll all tell you something useful, even in
what they elide</li>
<li>exploration process; code probe, proposing scenarios, proposing
models, talk talk talk</li>
<li>emphasize: must be able to make mistakes; in fact he stresses
that people need to come up with at least three bad ideas when
exploring with domain expert -- "most creative ideas are bad
ideas, at least at first"</li>
</ul>

<p>Toward end:</p>

<ul>
<li>idea you never look ahead beyond the next story is damaging;
not using your assets; some people are good at seting how
the little piece fits into the big picture -- let them!</li>
</ul>

<p>CMW: You need to iterate your learning about the domain just as
you iterate your learning about the implementation. (Probably
more.)</p>



