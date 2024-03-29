---
tags: grammar testing refactoring
layout: post
title: "Jester for English"
---



<p>
  <a href="http://jester.sourceforge.net/">Jester</a> is a fairly
  unique testing tool for the Java language. It calls itself a
  "mutation testing" tool and aims to find code that might be marked
  as covered in a code coverage tool but that code might only be
  executed, not tested.
</p>

<p>
  What Jester will do is introduce random changes to the code and
  re-run the tests -- if the tests still show green that means the
  code that was changed is either superfluous and can be deleted, or
  that you're not actually testing it. Both are great results to know.
</p>

<p>
  What I'd like to see is the same thing for the <b>English</b>
  language. How much superfluous and useless language have you seen?
  (How much have you seen on this website? Wait, don't answer that...)
</p>

<p>
  For instance, there's a sheet of paper in every meeting room at work
  with mostly commonsense guidelines. One of them has to do with food
  and drink, and it says: "Organization and cleanliness go a long way.
  Please be proactive in cleaning up after your meeting." What do you
  think Jester/English would do with that?
</p>


