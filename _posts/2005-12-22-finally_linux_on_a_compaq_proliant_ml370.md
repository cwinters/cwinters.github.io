---
tags: linux proliant
layout: post
title: "Finally: Linux on a Compaq Proliant ML-370"
---



<p>A few weeks ago <a href="http://blog.moertel.com/">Tom</a> offered up a machine one of his clients was giving away and I happened to be fastest on the 'reply' draw. It is a beast: tower configuration, three power supplies, three hot-swappable SCSI drives (with a few more bays) and a case made out of heavy lead or something. (It needs a new CMOS battery too, no big deal.)</p>

<p>At first I hauled it into work thinking that it would be an easy install: most linux installs are pretty simple nowadays. After a little while of fiddling I figured it wasn't going to happen (Compaq-specific hardware configuration) and I didn't want to burn anymore work time doing it, even if it was going to be tangentially useful for work. So I brought it home</p>

<p>I actually had another, more powerful, reason for bringing it home: it is really loud. Its normal home is a server room away from normal humans; in an office environment it's like a rocket. One of the folks at the Perlmongers meeting last week thought it might be because I only had two of the three power supplies plugged in, but it's not true -- I have all three plugged in right now and it's a racket.</p>

<p>Christmas and other goings-on have sidelined me but I finally got back to the machine this evening. It took a while to hit on the correct sequence of installation events but it's now grabbing a bunch of Debian packages for post-basic install.  (This is my first Debian install, just to see what it's like.) Here's what I did:</p>

<p><ul>
  <li>First: it's worth noting that the model name 'Proliant ML-370' is highly overloaded by Compaq/HP. This one is known as the '600-1000 mhz' model since that's the speed range of the P3 chip(s). (I'll <a href="http://h18023.www1.hp.com/support/files/server/us/family/model/1119.html?lang=en&cc=us&prodSeriesId=254940">save you the trouble</a> of drilling down into HP's site.) My model has two 733 mhz chips.</li> 
  <li>Grab the <a href="http://h18023.www1.hp.com/support/files/server/us/download/22678.html">SmartStart ISO</a> and burn it to a CD. I grabbed 5.5 just because it's what the previous owner used, but newer versions may be useful.</li>
  <li>Boot to the SmartStart CD and do a System Erase. Reboot.</li>
  <li>Back into SmartStart: mark the first non-array SCSI controller (the one with other drives attached) as first in boot order.</li>
  <li>Be sure to install the System Partition Utilities -- it's a special Compaq partition with their utilities as well as some special boot-up logic. (More on that in a bit.)</li>
  <li>There's a step in the sequence where you can mark what type of OS you're installing. I picked Linux, but I don't know if it actually makes a difference.</li>
  <li>Once all that's done you need to configure the array. I took the lazy way out and striped a big old RAID5 across all the disks.</li>
  <li>For this linux install I used the Debian net installation. It reminded me of a Redhat install from about eight years ago, but it worked really well. All relevant hardware -- including the Compaq Smart Array 5300 -- was detected with no problems, it picked up DHCP from my internal router, saw the other SCSI drives. Hooray.</li>
  <li>I setup <tt>/boot</tt> on the first available partition on the first non-array SCSI drive and made it bootable. Since it was on the first controller it was marked as <tt>/dev/sda</tt>. Be sure not to overwrite the Compaq partition already there, and note that they did something weird by making that Compaq partition #3 even though it was created first. (This tripped me up once.)</li>
  <li>One trick to the install: DO NOT allow GRUB to overwrite the master boot record. (I assume this applies to LILO as well if you're using that.) The installer will ask you if you want to do so and give you a little "It's okay" nudge because it didn't find any other operating systems. Instead, I installed to <tt>/dev/sda1</tt>. (Remember: even though <tt>/boot</tt> was installed second it's marked as the first partition.)</li>
</ul>

<p>After a reboot you'll get the crazy-long SCSI bootup procedure and then it'll ask you something like, "Press F10 for System Partition Utilities" If you wait it'll drop to the first bootable partition which is where it'll find GRUB's boot record and get everything rocking. Debian went though what must be its normal installation procedures and, like I said, is downloading packages as I type. The only hitch in that was the bizarre locale choice screen: it selected a good default, but I had no idea it had done so and had to scroll down a curses-list of about 800 other locales with inscrutable codenames. Feh.</p>

<p>BTW, I actually did try the Gentoo LiveCD install with this, but it kept barfing up weird SQUASHFS errors, probably because it couldn't find some hardware even though I gave it the 'doscsi' boot parameter. Oh well.</p>


