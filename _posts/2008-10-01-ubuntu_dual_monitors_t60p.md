---
tags: ubuntu linux thinkpad
layout: post
title: "Dual Monitors with Hardy Heron + T60p"
---

A [couple months ago](/2008/07/26/upgrading_to_hardy.html)
I wrote about upgrading to Ubuntu 8.04 on my
T60p. And in that I referenced that I could get the 'big desktop'
working but rudely didn't follow up with how. Bill de hÓra
mentioned on twitter difficulties with getting this working,
unknowingly nudging me into action.

First, follow 
[this user's instructions](http://jwylie.blogspot.com/2008/06/ubuntu-804-on-my-thinkpad-t60p-part-2.html)
and use EnvyNG to install the relevant ATI
driver. (It will probably work if you use something else to install
the driver, but I can't verify that.)

Fire up a terminal and run the ATI config tool to see which
monitors the video card thinks are connected. If I run this with
no external monitors I get:

<pre class="sourceCode">
cwinters@potomac:/home/cwinters$ <b>aticonfig --query-monitor</b>
  Connected monitors: lvds
  Enabled monitors: lvds
</pre>

The 'lvds' is always your laptop display panel. If you now connect
an external monitor (including a projector) directly to your laptop
you'll see:

<pre class="sourceCode">
cwinters@potomac:/home/cwinters$ <b>aticonfig --query-monitor</b>
  Connected monitors: lvds, crt1
  Enabled monitors: lvds
</pre>

If you want to use display that monitor to display you need to
enable it; this requires <tt>sudo</tt> access since you're
rewriting your X configuration for next time:

<pre class="sourceCode">
cwinters@potomac:/home/cwinters$ <b>sudo aticonfig --enable-monitor=crt1,lvds</b>
[sudo] password for cwinters: <b>********</b>
</pre>

This should flicker both displays. If the external display is the
same resolution as your laptop display (mine's 1600x1200), you'll
now have a mirrored version of your desktop. Cool!

To display the big desktop, Click 'System | Preferences | Screen
Resolution...'. There should be a new option available, like
'3200x1200,' indicating a desktop as twice as wide as what you're
using now. Choose that then click 'Apply'.

If things are working you'll now see an empty desktop on your
external display. Click the 'Keep changes' button on the
confirmation that pops up.

When you unplug the external display, just go back to the 'Screen
Resolution' applet and change your resolution back to whatever
your laptop panel supports.

If you have a dock and want to display and two external monitors
at once, that's doable too. First, when you start your T60p in the
dock go into the BIOS and tell the display to work on
'DVI+VGA'. Restart. The pretty Ubuntu boot sequence may show up on
both monitors but it won't last. Eventually your boot sequence
will show up on either your laptop (if it's open) or one of the 
two monitors. Login as normal and fire up a terminal, then see 
what the laptop thinks are connected again:

<pre class="sourceCode">
cwinters@potomac:/home/cwinters$ <b>aticonfig --query-monitor</b>
  Connected monitors: lvds,crt1,tmds1
  Enabled monitors: lvds
</pre>

This assumes you're still viewing the display on the laptop
panel. If one of the other displays is lit up you'll see something
different. Now, just like before:

<pre class="sourceCode">
cwinters@potomac:/home/cwinters$ sudo <b>aticonfig --enable-monitor=crt1,tmds1</b>
[sudo] password for cwinters: <b>********</b>
</pre>

You should now be seeing a mirrored desktop on both displays. Do
the same trick as above for displaying the big desktop with the
'Screen Resolution' applet.

Regarding positioning: I was never able to reliably tell via
software which monitor should be on the left and which on the
right. IME the DVI monitor always wants to be monitor 1, so I just
plugged that in on the left and the VGA on the right and
everything worked. (There's probably a way to do this, but I just
want it to work.)   

Sometimes when you dock with the lid closed and turn on the
machine you won't get any display on either external monitor. When
this happens, open up your laptop and you'll see the login
screen. Login as normal, then execute the '--enable-monitor' steps
above.

I have also not been able to suspend while docked, undock and have
anything good happen. The reverse doesn't happen either, and it's
one of the things WinXP did mostly well.



