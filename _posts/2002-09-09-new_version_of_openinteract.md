---
tags: programming
layout: post
title: "New version of OpenInteract"
---



OpenInteract 1.51 is on the loose, and of course you're soaking in it :-)

<p>One problem I just encountered that I hadn't previously thought about -- I might need to build in a check to see if the user is an administrator when checking/filling the cache. Because administrators and normal users in some cases see different things. (For instance, on the front page I get a small 'Edit' link next to each news story.) But if I'm the first person to look at the page, then <b>everyone</b> sees the 'Edit' link.</p>

<p>It's not a security problem (you'd just see the static, noneditable version of the object), but it's bad programming to let people see options they might not even be aware of.</p>

<p><b>Update</b>: This is updated in CVS so that if a user is an administrator:<br>
<tt>if ( $R-&gt;>{auth}{is_admin} )</tt><br>
then this user neither reads from the cache nor writes to the cache. This is a kludge, however. I'll devote a low-priority thread to it :-)</p>



