---
tags: perl
layout: post
title: "Observable"
---



<p>Forgot to mention this: I had an excellent idea on the bus today about making SPOPS rules use the Oberver pattern rather than the current setup which uses the "pulled out of my ass" pattern. This does a 180 on the current flow -- notifying classes on actions rather than having those classes push code at gen time to run on actions -- but it makes it possible to take the generated class and serialize it for later. We can't do that now since we're shuffling coderefs around.</p>

<p>Unfortunately, this will likely break backward compatibility. On the bright side, there are probably only a handful of people using rules right now :-)</p>


<p><em>(Originally posted <a href="http://use.perl.org/~lachoy/journal/4553">elsewhere</a>)</em></p>


