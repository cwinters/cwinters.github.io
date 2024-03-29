---
tags: programming
layout: post
title: "XP chatter"
---



First Chiara <a href="http://www.freeroller.net/page/chiara/20030119">pounded on pair programming</a>, with multiple exclamation points. (Unfairly too:  if Kent Beck doesn't have the expertise to discuss this, then I don't know who does.) Then <a href="http://freeroller.net/page/cbeust/20030121">Cedric offered</a> a more resonable argument, outlining the management objects and, more importantly, the social roadblocks:

<blockquote>Mental dissonance, first.  Even if both developers have similar backgrounds and a similar amount of knowledge (already an impossibility in my opinion), there is still the problem that both of you will have different ways of solving the problem.  Granted, you might eventually agree on a common solution if both are open-minded (another requirement) but it's going to take a lot of discussing before reaching that point.</blockquote>

<p>But then <a href="http://crazybob.org/roller/page/crazybob/20030119">Bob responds</a> to the Chiara's post with:</p>

<blockquote>I have a feeling that most of the people who are emphatically against PP are just really not comfortable doing what they do in the privacy of their own cube in front of another teammate. You have to drill down to the root of this discomfort. Do they have social, teamwork issues? Are they doing something they shouldn't? Are they not truly comfortable with the quality of their code? Pair programming can rememdy all of these situations, turning a group of would be strangers with thrown together silos of code into a tightly knit team with a collectively owned code base. You become a better public speaker only by speaking in public, not by talking to yourself. You become a better teammate by working with your team.</blockquote>

<p>At work we're at the start of implementing pair programming for all our future development. I can see Cedric's point, but at least for our organization there are other factors weighing in. The primary of these: we have to get rid of module (or package, or subdomain) provincialism. This occurs when a developer only really knows and can work on the code that she created and worked on before, and in a large system it can be crippling. Documentation doesn't do it, because people don't write it and even if they do it gets neglected and out of date. (And incorrect documentation is usually worse than no documentation at all.) Code review doesn't do it because you wind up running into many of the same social issues that Cedric outlined.</p>

<p>There definitely are social issues, particularly for people who are used to doing everything alone. And being at different skill and knowledge levels can make progress stop-and-go, but this will hopefully diminish over time as people get better. (You really need to take off your nitpicky cap to help this happen, not worry about critiquing the small things.) But I see the pair programming process as making the whole team better rather than relying on a few workhorses. Particularly in a small company, where if the workhorses quit development would be set back at least six months.</p>

<p>Interestingly, our development management is fully committed to pair programming, primarily because of direct experience with the benefits. We'll see how the whole thing goes.</p>


