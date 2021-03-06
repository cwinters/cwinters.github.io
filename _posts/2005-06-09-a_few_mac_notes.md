---
tags: gentoo mac
layout: post
title: "A few mac notes"
---



<p>I recently upgraded to 10.4 and in general it went pretty well. I couldn't jump in when all the cool blogkids did since Barb wasn't yet done with her school paper and I didn't want to keep PageMaker on there, nor did I want her to run into any issues with upgrading.</p>

<p>Typically when upgrading an OS I'll do a backup, wipe the disk, then fresh install. It takes quite a bit longer but it forces you to only keep the applications you need. However, I didn't have that option this time. The installer kept complaining about a problem with the disk catalog, and neither the 10.3 nor 10.4 Disk Utility could fix it -- actually, the 10.3 one didn't even see there was a problem.</p>

<p>The other issue I ran into was with memory. I <a href="http://www.cwinters.com/news/display/3257">bought some</a> third-party memory a while ago and it worked well except for two times -- booting the computer and sleeping. Sometimes the startup sequence would hang, but after two or three restarts it went okay. With sleeping, I couldn't just close the lid of the powerbook because it would never wakeup -- using AppleMenu->Sleep worked fine though, and the money saved made this a decent tradeoff.</p>

<p>But it doesn't work <b>at all</b> with Tiger. Not only did the installer refuse to start, but after everything was installed I tried to use the newer memory again -- no boot. So now I'm back to 512 and have a useless GB stick of memory. (Onto ebay you'll go!) Last night <a href="http://www.caseywest.com/">Casey</a> mentioned a place where he picked up 2 GB for his powerbook for something like $450 -- nice!</p>

<p>Since I did a fresh install I could take a new look at package management tools. I remembered that <a href="http://www.gentoo.org/doc/en/macos-guide.xml">Gentoo</a> ported portage/emerge to OS X and checked it out. Installation was fine, but eventually I realized that some of the packages I really want weren't supported in macos:</p>

<p align="center"><img src="/images/blog/gentoo-osx-no-xemacs.png" alt="No XEmacs on Gentoo..." /></p>

<p>So: adios Gentoo! Back to fink I went.</p>

<p>Other than that things seem to work pretty well. I don't think Searchlight will be a replacement for LaunchBar (or QuickSilver) because it seems to be focused on indexing rather than launching. My reason for thinking this? I launch Quicken every few days and it takes 5-6 seconds -- an eternity! -- for the Quicken app to show up. But some of the data files show up immediately.</p>


