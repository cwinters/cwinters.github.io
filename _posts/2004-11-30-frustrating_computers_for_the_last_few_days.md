---
tags: daily-life
layout: post
title: "Frustrating computers for the last few days"
---



My mail/web server -- which also hosts the OpenInteract stuff (wiki/JIRA) -- was off the net for the last day or so, some sort of networking problems with my hosting provider. Since it's in Maryland and hosted for free my hands are pretty much tied when something like this happens -- but the trade-off is generally worth it. Forcibly being away from email for so long is fairly painful. (Sign of an addict when 24 hours is "so long"...)

<p>The other problem was upgrading my IMAP server due to <a href="http://www.gentoo.org/security/en/glsa/glsa-200411-34.xml">security concerns</a>. Mostly due to cyrus linking against different versions of Berkeley DB the older versions not being around, etc. What a PITA -- and getting SASL to work properly again was painful too. (People wonder why everyone recreates the wheel...)</p>

<p>I wound up just blowing away the mailboxes.db file, getting cyrus to create an empty version, then running a quick Perl script to recreate everyone's mailboxes. (I found out shortly after that I could have just used 'reconstruct' to do this -- doh!) The only problem: in also blowing away the 'user.seen' databases all messages were marked as new. Boo!</p>

<p>I did have a very productive Saturday with OpenInteract and got it pretty much ready for a hugely overdue 2.0 beta 5 release -- you're soaking in it right now, actually. Sunday I used a circular saw for the first time -- and I still have all my fingers!</p>

<p>(update: fixed typo...)</p>


