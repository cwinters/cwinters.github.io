---
tags: programming
layout: post
title: "Translate your cron entries into english"
---



<p><b>Update:</b> Just in case it's <a href="http://www.htmlism.com/mark/archives/002791.html">not clear</a>, I didn't write this script, the amazing <a href="http://interglacial.com/~sburke/">Sean Burke</a> did.</p>

<p><a href="http://www.cpan.org/authors/id/S/SB/SBURKE/crontab2english_0.71.pl">crontab2english.pl</a> - Extremely useful utility -- in Perl, of course -- for ensuring that you have the correct time specification in your crontab. For instance, after downloading, copying to <tt>/usr/local/bin</tt>, chmod'ing, and stripping the file extension I can do:</p>

<pre class="sourceCode">
cwinters@www cwinters $ crontab2english
...
Command: (line 7)
  Run: /usr/bin/wget -O 
   .../openinteract-cvsroot-`/bin/date +%Y-%m-%d`.tar.bz2 
   http://cvs.sourceforge.net/cvstarballs/openinteract-cvsroot.tar.bz2
  At: 8:10am    every day

<p>Command: (line 8)
  Run: perl /home/cwinters/bin/cleanup_backups /home/cwinters/oi_backup
  At: 0:10am on    the first of    every month
</pre>


