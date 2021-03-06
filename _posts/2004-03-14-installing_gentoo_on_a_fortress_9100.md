---
tags: technology
layout: post
title: "Installing Gentoo on a Fortress 9100"
---



Just a couple of notes on installing <a href="http://www.gentoo.org/">Gentoo Linux</a> (2004.0) onto a <a href="http://english.aopen.com.tw/products/server/baresystem/ft9100.htm">Fortress 9100</a>. (Some of them apply to any distribution, but that's your problem.) The install was fairly painless and mostly by the book. But...
<ul>
 <li>Before you start: the onboard SCSI adapter will detect SCA drives from right to left, so the drive in the right-hand slot will be <tt>/dev/sda</tt>, the drive in the left-hand slot <tt>/dev/sdb</tt>. (Or more specifically, the SCSI adapter will assign LUN 0 to the right-hand slot, LUN 1 to the left-hand slot.) I don't know if it does this for non-SCA drives. Be sure you've got the drives in the right place before you start the install.</li>
 <li>Booting from the Gentoo 2004.0 LiveCD works fine (I used the 'Universal' one optimized for P3); when asked for boot options, I used: <tt>smp nohotplug doscsi</tt>. 
For some reason something seemed to hang in the hotplug detection the first time.</li>
 <li>The boot process did not detect the dual onboard ethernet ports, likely because 'nohotplug' specified, so once you're booted issue a <tt>modprobe eepro100</tt> and both will get detected.</li>
 <li>Since the network ports didn't get detected the network wasn't automatically setup. I was behind a DHCP router so I just setup the network with <tt>net-setup eth0</tt>. (BTW, <tt>eth0</tt> is the LAN port on the power input side)</li>
</ul>
<p>Everything else goes as normal, just follow the excellent <a href="http://www.gentoo.org/doc/en/handbook/handbook.xml?part=1">Gentoo installation instructions</a>.</p>


