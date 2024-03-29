---
tags: solaris unix
layout: post
title: "Impressions of OpenSolaris"
---



<p>I've been using a build of <a
href="http://developers.sun.com/sxde">SXDE</a> as my primary work
machine for about the last month. The reason is to get used to Solaris
since we'll be deploying our application on it starting sometime this
year -- I haven't been even a fake sysadmin for years, and that was on
Linux.</p>

<p> Since I'm using a laptop (Thinkpad T60p) and WinXP, I took the
relatively safe way out and installed a second hard drive in the ultra
bay for Solaris. Because the ultra bay is taken up you need an
external CD/DVD drive for installation, but USB works fine.</p>

<p>I haven't been taking notes for the whole time, so this is off the
top of my head:</p>

<p>First surprise: installation was slick and easy. I'd installed
Solaris 10 on a spare PC a while ago (year?) and it was fairly
primitive, reminding me of linux installs 10 years ago.</p>

<p>Next surprise: wireless just worked. If it doesn't see a wired
connection it'll pop up a little applet with the networks it sees and
the security for each. (There's no 'Stop looking!' button, but that's
minor.)</p>

<p>After that, it's been mostly great, with a few notable ups and
downs:</p>

<p>Downs</p>

<ul>

  <li>Up <a href="http://www.cwinters.com/news/display/3617">until
  about two hours ago</a> I couldn't VPN in to work. If this wasn't
  fixed it probably would have been the single biggest reason to stop
  using Solaris, Most of the time getting email through a web
  interface is sufficient, but other times I really need access to
  perforce.</li>

  <li>No suspend/resume. One of the biggest advantages of using a
  laptop is that I can open it and immediately start doing
  something. I never have to turn it off. Well, when I used Windows on
  this machine I didn't. Now I do. It's annoying.</li>

  <li>Something about power management or fan control isn't working
  properly, because I can freeze (sometimes reboot) this machine under
  load. And using the 'batstat' program I can see the temperature
  going up up up until it's two or three degrees below critical for
  one of the thermal zones, then =pow!=, it's gone. This happens more
  easily while the machine is docked (I think because there's no air
  passing under the machine to carry away heat), but it can happen
  when it's sitting on my iCurve as well, it just takes a little
  longer. It's possible this is a result of using the ultra bay hard
  drive as the primary one, but I dunno.</li>

  <li>I really miss a QuickSilver/Launchy-type application. I know
  there's a couple for GNOME (like <a
  href="http://do.davebsd.com/">GNOME Do</a> or <a
  href="http://developer.imendio.com/projects/gnome-launch-box">GNOME
  Launch Box</a>), but they or their dependencies have problems
  building. Most GUI stuff treats non-Linux systems as an
  afterthought, but they'll eventually be supported (probably).</li>

  <li>Multiple-monitor support. On Win32 in the dock I can drive 2 20"
  panels from the laptop. And even if it's not in the dock I should be
  able to display on both the single external VGA port and on the
  built-in LCD. And plugging into a projector? Ha!

  <p>This laptop has an ATI FireGL 5200
  chipset. Unfortuntely it's not nVidia, which is apparently more
  common and more easily supports these crazy use cases.</p>
  </li>

  <li>It's heresy, but I miss Outlook a little. When I first saw
  screenshots of the vertical three-pane view I didn't like it, but
  after using it a bit I'm hooked. The three-pane view in Thunderbird
  is just okay, it doesn't show enough information in the middle pane
  (listing view). And while there is some basic calendar support in
  Thunderbird it's one way -- I can't confirm appointments, just add
  them to my calendar. (Evolution does support Exchange, but it's been
  flaky.)</li>

  <li>We have fairly arcane methods of getting to some of our client
  sites, and some of them (based on Citrix) are Win32
  only. Annoying, but not Solaris's fault.</li>

</ul>

<p>Ups</p>

<ul>

  <li>Ahh, back to unix. Everything else is pretty much gravy.</li>

  <li>My daily work (compiling, editing, running) is faster. Something
  that took a minute on Windows takes 20 seconds.</li>

  <li>ZFS is freaking magical</li>

  <li>Most everything I used in Win32 (which isn't much) has a good
  equivalent: IM, basic image editing, screenshots, Java IDE, xemacs,
  web, Postgres, remote desktop.</li>

</ul>

<p>That should do for now, more things will probably pop up later.</p>



