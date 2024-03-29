---
tags: qcon conference javascript ajax ui opensocial security oauth
layout: post
title: "QCon 2009: OpenSocial in the Enterprise"
---



<p><strong>Tim Moore, Atlassian</strong></p>

<p>Problem:</p>

<ul>
<li>JIRA dashboard renovation for 4.0</li>
<li>Enterprise apps are silos: too many dashboards</li>
<li>Need a global view that combines data from different
instances of the same app</li>
<li>Also need to bring in view from other vendors</li>
</ul>

<p>Orient dashboard to team, not tools team is using.</p>

<p>Geared toward standard way to share social data among apps (e.g.,
Facebook apps).</p>

<p>Published in standard: OpenSocial Gadgets</p>

<p>Three main parts:</p>

<ul>
<li>Data model: people, activities, relationships</li>
<li>Web service APIs (RESTful)</li>
<li>Gadgets: sites tat publish, sites that consume</li>
</ul>

<p>Gadget doesn't need to know where it's displayed</p>

<p>Spearate them from one another with IFRAME so a single gadget
doesn't "take out" the page with poor performance, bad markup, or
hostile intent. Sandboxing gets around problems people saw with
portlets, which were entirely server-side.</p>

<p>Based on (or "inspired by") Google's 'iGoogle' gadgets </p>

<p>Write once, display anywhere. (Mostly...)</p>

<p>Securith: uses OAuth</p>

<p>Reference implementation: Apache Shindig; Java + PHP
implementations; contributed originally by Google</p>

<p>Anatomy of gadget:</p>

<ul>
<li>XML spec file (generally static)
<ul>
<li>metadata (who wrote, category, description)</li>
<li>HTML for display</li>
<li>Javascript</li>
<li>Since container can aggressively cache, spec file should
not be user-specific </li>
</ul></li>
<li>Core JS API: access user preferences, make requests</li>
<li>Features: what features are required by this gadget of its
container; can reference container-specific APIs</li>
</ul>

<p>nice architecture diagram: Browser -> Container -> Gadget
server</p>

<ul>
  <li>container has request proxy so that AJAX requests will work
      properly, since the gadget needs data from a server different
      than the one serving the gadget up.</li>
</ul>

<p>Spec:</p>

<ul>
<li>'Require' of 'feature' items</li>
<li>User prefs: how can the user control content? enough metadata
to create simple API to elicit user info</li>
<li>Content: HTML with references to CSS, JS; JS uses API to
display message</li>
</ul>

<p>Requesting data from WS</p>

<ul>
<li>use AJAX + DOM (duh)</li>
<li>later versions of OS have templating, tags</li>
<li>Use of OAuth <strong>central</strong></li>
<li><code>gadgets.io.makeRequest()</code> deals with async magic; includes
ability to autoparse response into DOM (from XML) or JS object
(from JSON)
<ul>
<li>REST server-side APIs most convenient and used</li>
<li>OAuth triggered by params passed to <code>makeRequest()</code></li>
</ul></li>
</ul>

<p>Enterprise readiness/downsides</p>

<ul>
<li>No SSO; security concrens; OAuth not implemented in many places
(yet); finding ways to make this work, but in proprietary ways;
also "two-legged OAuth" being done (but user credentials must
exactly match)</li>
<li>assumes big container (google, linkedin), little app servers
<ul>
<li>implies hub-and-spoke model vs many connected apps</li>
<li>configuration not so straightforward (assumes you are big
container and do this often)</li>
</ul></li>
<li>running behind firewall
<ul>
<li>deployment issues: assumes two-server setup to enforce some
security via browser cross-domain restrictions (so gadget A
cannot pickup gadget B cookies)</li>
<li>many assume they're on public internet, use google
analytics etc.; when behind FW they fail, degrading
ungracefully</li>
</ul></li>
<li>portable gadget: what if you cannot hardcode URL in your gadget
spec b/c it might change? (e.g., my instance of JIRA) Atlassian
developed templating language to allow substitution of certain
variables within the XML spec -- typical bootstrapping problem</li>
<li>no 1.0 spec yet; shindig still in incubator</li>
<li>still compatibility issues for gadget authors, especially cross
container </li>
<li>coming: PubSub, ability for gadget to publish a message to a
known channel and other gadgets to get the message and update
themselves accordingly</li>
<li>Caja: safer JS + CSS, allows you to get rid of IFRAME; problem:
doesn't work with major JS frameworks (I'm a little dubious of
this) </li>
<li>SocialSite: extensible OS container</li>
</ul>



