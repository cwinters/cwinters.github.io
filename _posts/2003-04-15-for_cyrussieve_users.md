---
tags: technology
layout: post
title: "For cyrus/sieve users"
---



If you try to run <tt>sieveshell</tt> and get the following error:
<pre class="sourceCode">
$ sieveshell -a myuser localhost
connecting to localhost
Bad protocol from MANAGESIEVE server: EOL2
</pre>

<p>You might check to see if:</p>

<p><ul>
  <li>Your user has a directory (owned by cyrus.mail, of course) in the configured <tt>sievedir</tt> found in <tt>/etc/imapd.conf</tt>. This is normally <tt>/var/imap/sieve</tt>. The directory will be under another directory of the username's first letter. (It'll be obvious when you see it.)</li>
  <li>You do not have both <tt>sievedir</tt> set and <tt>sieveusehomedir</tt> set to 'yes'. I had the above problem and changing the latter to 'no' made everything happy.</li>
</ul>

<p>I wouldn't normally post something this trivial, but google gave me no help when finding an answer, so this is for myself 18 months from now when we're reconfiguring cyrus...</p>


