---
tags: oi2 perl releases
layout: post
title: "Almost got another release out"
---



Finally, only a few months late, another release of the OpenInteract2 beta will be going out the door shortly. It's got way too many feature updates for a single beta release, I know. But putting out a release is a fairly serious time commitment. Not for the actual release, but for the week or two afterward where you'll probably get more questions than usual about installation, functionality, etc. And I've been either tied up with real life stuff or a little burned out to commit. Plus I kept adding features...

<p>Anyway, this site is already running on the CVS version from a couple of days ago. One of the features I added (or fixed) was action types. It's typically an action that needs nothing but configuration -- the lookup table editors shipped with the server are one, the template-only actions are another. Those are kind of boring though. Why not jazz it up with a buzzword? And that buzzword is: RSS!</p>

<p>So on the main page of the site you'll see a 'Recent Links' box. Here's all I had to do to add the <tt>OpenInteract2::Action::RSS</tt> perl module (on CPAN as soon as this beta is released), add this template code to the home page:</p>
<pre class="sourceCode">

</pre>
<p>and add the following action so that box has some content:</p>
<pre class="sourceCode">
[delicious_links]
action_type  = rss
feed_url     = http://del.icio.us/rss/cwinters/
title        = Recent Links
cache_expire = 180m
template     = my_custom::delicious
url_none     = yes
weight       = 2
num_display  = 8
</pre>
<p>Most of that is pretty easy to follow I think. Of the stuff that isn't:</p>
<ul>
  <li>'template' uses the OpenInteract syntax for finding a template -- that's the 'delicious' template in the 'my_custom' application package
  <li>'url_none' says that this action shouldn't be accessible by URL
  <li>'weight' refers to how the box is sorted.
</ul>

<p>Caching is done automatically by OI2 actions so all we need to do is specify how long we want the content to stick around.</p>

<p>I also have an implementation of lightweight object tags a la delicious so you can use the same tags to reference any object on the site -- you can actually see the box at the <a href="http://www.cwinters.com/programming/">programming</a> page -- but I'll talk more about that later.</p>


