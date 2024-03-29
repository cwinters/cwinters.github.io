---
tags: mac perforce
layout: post
title: "Unusual perforce download"
---



<p>One of the useful things about Perforce is that since they use server-based licensing you can download the client whenever you want. For instance, if you wanted to check the WORA status of your server-side Java framework by building and running it on your Powerbook you could just go to the <a href="http://perforce.com/perforce/downloads/macosx102ppc.html">Mac download page</a> and grab one of the clients there, set a few environment variables and be on your way.</p>

<p>The unusual thing is this: the first download is described as "P4 (Perforce Command-Line Client)", and they mean it. You don't get a tarball or zip file with a README, help file, release notes, etc. You just get a binary called 'p4'.<sup>1</sup> That's it, very clean, very simple. The binary comes with built-in ample documentation from 'p4 help', and honestly, who actually reads the release notes with every download? You'll just read them if you have a problem, and in that case you can grab them online from the same download page.</p>

<p><sup>1</sup> And at least with Safari you'll need to manually do the 'download link to file' action otherwise you see it directly in your browser. </p>


