---
tags: apache cwinters.com sysadmin
layout: post
title: "Weird apache errors after upgrade"
---



<p>Gentoo has been <a href="http://www.gentoo.org/doc/en/apache-upgrading.xml">updating their Apache ebuilds</a> and as a result of a recent upgrade my static Apache was kinda broken. "Kinda" in that the proxying function worked -- my site was fine, and the images (and feeds) were served statically just fine as well. But some of the other virtual hosts segfaulted the Apache child on any request -- even the drop-dead simple one for my wife's tutoring website segfaulted, and there's nothing there!</p>

<p>I didn't even realize this was happening for ~ a day, so the openinteract.org web server was down, but oddly the issue tracking system wasn't (since it sits behind a proxy). Rather than see what was going on with the Apache (no patience), my fix was to just build another Apache by hand -- still in muscle memory despite not doing admin work for a few years. The only problem is that I need to build mod_php and mod_ssl (for Squirrelmail), and doing that has always given me pause because of the headaches over the years. (Yet another reason to hate PHP, sorry Kirk.) Maybe it's better now, we'll see...</p>


