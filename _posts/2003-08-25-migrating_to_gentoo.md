---
tags: technology
layout: post
title: "Migrating to Gentoo"
---



Last weekend I migrated my web/mail server from Red Hat 7.1 to Gentoo 1.4. It was down longer than expected, partly because of a trip to Erie (wear sunscreen even if it's cloudy!), but also because of some hiccups that overwhelmed the smooth parts (It's taken me a while to write this up so some details may not be fresh in my mind, sorry.)

<p>First, though I mentioned this <a href="/2003/04/15/helpful_hints_for_major_upgrades.html">before</a> (ironically, another migration from RH to Gentoo) it's worth reiterating: it's extremely useful to backup entire directories to a separate hard drive rather than either individual files or to a tape drive. It doesn't matter if the drive is slow or whatnot, it's just easier than digging through a tape of stuff.</p>

<p>Next, it's important to <a href="http://homepage.mac.com/rjschwarz/jedi.html">trust your feelings</a>. It something is bothering you and you have some experience in these things, don't assume that the quick answer is the best. In my case, when booting off the Live CD I'd choose the default Gentoo kernel and options and get a blank screen. This <b>seemed</b> to be a framebuffer problem based on what other people were saying, but this struck me as odd because the video card is supported extremely well under Linux (Matrox Millenium II). Oh well, what do I know, something wonky is probably going on so I'll just try passing a 'vga=normal' to the kernel. This just masked the problem.</p>

<p>So if your machine is year or two old it's probably a good idea to upgrade your BIOS before doing anything. (The <a href="http://english.aopen.com.tw/products/mb/AX64Pro.htm">AX64 Pro</a> BIOS is up to 1.10, I had 1.00.) This caused me major, major headaches with booting off the LiveCD. I'd get errors like 'Uncompressing Linux... crc error --System halted" and other similarly inscrutable errors. I figured it was something to do with the new CD burner that's so lazy it can't get its door open without a little help -- maybe I'm burning the CDs at too fast a speed? I'll try them at 16x. Oh, that didn't work, try 8x. Try passing a 'nousb noraid nothis nothat' set of parameters...</p>

<p>Well, accidentally or no, one time it worked and I got the initial install complete -- stage 3 unpacked, main packages emerged, kernel built, GRUB installed. A reboot to move to the next stage and... gah! Kernel panic! Oh well, try to boot again off the CD since I probably fudged a GRUB setting. Gah: 'crc error'! Bastard! Time for sleep...</p>

<p>I woke up and upgraded the BIOS (learning that you can make an MS-DOS bootable floppy from Windows XP), and then the machine booted happily from the CD, twittering away. A quick fix of the GRUB setting (at least I was right about something) and it booted.</p>

<p>Not that it booted properly -- iptables wasn't working properly so the firewall wasn't up. (It is now, don't get any ideas...) But at least networking was up so I could continue some compiling from work. Since the website was already up (that's easy, I can do that in my sleep) the next step was email. And the first part of that is to get cyrus up and running so sendmail has something it can deliver to. Unfortunately I hadn't taken a backup of my <tt>/var/imap/mailboxes.db</tt> -- that is, a backup in the 'dump it out to a sane format' sense rather than the 'backup the file' sense. Oops. And since I was upgrading from 2.0.16 to 2.1.14 that's necessary. A little (well, a lot) of futzing and prodding I finally coerced the old mailboxes db into a reasonable format so <tt>reconstruct</tt> could work ok. Bing, back up.</p>

<p>Next step is sendmail. I learned that Gentoo helpfully installs <tt>ssmtpd</tt> into <tt>/usr/sbin/sendmail</tt> for you, so all your scripts with a hardcoded path to the mailer will still work. (WTF are you doing passing args to sendmail anyway instead of using a module? Oh, whatever...) That's despite the fact that I'd actually <b>emerged sendmail myself</b>. I thought that the binary was actually sendmail, especially since the init scripts were installed as well. So I kept trying to start it up again and again, tweaking the .mc file here and there and everywhere. Then I somehow saw what happened, re-emerged sendmail and started it up. Blammo.</p>

<p>After that, just issue an <a href="/2003/08/20/flush_specific_messages_from_sendmail_queue.html">impatient queue flush</a> to a server a couple states away and watch the spam roll in. Yahoo!</p>

<p>The only issue left was with iptables, and a few iterations back and forth finally sorted it out. Don't ask me what I did, but I wound up keeping them as modules (rather than compiling them statically), and you need to keep recompiling iptables to match your kernel.</p>


