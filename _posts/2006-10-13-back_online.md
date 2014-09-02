---
tags: cwinters.com
layout: post
title: "Back online!"
---



<p>My box was wedged for at least a week recently. I think the cause was a typo in a cron script -- it wasn't cleaning out a directory full of lock files, and even though I'm using reiserfs and SCSI the directory eventually became full enough to slow the machine to a crawl. How full? Once the machine was restarted, deleting the directory full of zero-byte files took about two hours.</p>

<p>The cron directive has been fixed, so hopefully  that won't happen again...</p>


