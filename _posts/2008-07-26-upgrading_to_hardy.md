---
tags: linux thinkpad ubuntu
layout: post
title: "Upgrading to Hardy"
---




<p>I have a presentation on Monday where I'm talking about what we've
done for the past two years. I think a lot of people are coming[1],
and it would be nice to use my Ubuntu install vs Windows. (Why? All my
little work crumbs aren't on Windows anymore, and if I need one during
the presentation it'll be awkward.)</p>

<p>Unfortunately, I've been lazy thus far and not played around enough
with the video to be able to use a projector. I heard that the T60p
has better support under the 8.04 Ubuntu release, so I stuck it on an
extra partition on the drive, then mounted my old <tt>/home</tt> under
that.</p>

<p>Notes thus far:</p>

<ul> 

<li>Install was typically easy, even though I was installing to a
  non-standard partition. (If the SXDE build of Solaris was so easy I
  wouldn't have lost data a few months ago.) It also detected the 7.10
  install and made it available via GRUB.</li>

<li>I found 
<a href="http://jwylie.blogspot.com/2008/06/ubuntu-804-on-my-thinkpad-t60p-part-2.html">this user's instructions</a> 
and used EnvyNG to install the relevant ATI driver. I had a little
trouble finding the GUI configuration tool (it's
<tt><b>amd</b>cccle</tt>, not starting with 'ati'). Using this and
setting the T60p bios to display on 'VGA+DVI', I was able to get the
'big desktop' on two external screens. But playing around with it
(changing the orientation) didn't work so well, and I didn't have time
to experiment before the end of the day came. (I'll post more about
that, as well as getting it to work on a projector.)</li>

<li>Even after getting the 'big desktop' working, I'm not sure how to
turn it off when I'm not in the docking station and have only the
laptop panel. It seems to think there should be another desktop there
('scaled' wallpaper is half off the screen, the mouse pointer doesn't
stop at the edge, etc.) but I'm not sure why. I know this stuff is
hard with different video manufacturers/drivers/etc., but it's still
awfully frustrating. It feels like it should be a solved problem by
now. (And maybe it is, I'm just ignorant of the solution.)</li>

<li>I'm using OpenOffice for the presentation, so I fired that up
quickly. It complained about not finding a JRE, which is weird, but no
effects I've seen so far. I noticed that OpenOffice has been
upgraded (from 2.3.x to 2.4.x), but it was reading my old preferences
from <tt>.openoffice2</tt>, which included the location of
Java. (Ubuntu comes with a layer of symlinks for this so you can
upgrade to minor versions without a problem, but OO didn't respect
that, using <tt>/usr/lib/jvm/java-6-sun-1.6.0.03</tt> instead of
<tt>/usr/lib/jvm/java-6-sun</tt>.)</li>

<li>With this upgrade I'm using plain old GNU Emacs. I'm not what
anyone would call a heavy Emacs user, but I've been using XEmacs for
so long that it's become a habit without a reason. A few months ago I
read about 
<a href="http://steve-yegge.blogspot.com/2008/03/js2-mode-new-javascript-mode-for-emacs.html">Yegge's new JavaScript mode</a>
but couldn't use it, because it explicitly doesn't work on XEmacs. So
with this upgrade I'm not even putting XEmacs on the system. I
probably won't even notice, since most of the auto-invoke stuff (like
the 'P4EDITOR' env) uses 'gnuclient' instead of 'xemacs'. I really
need to learn to use my editor better.</li>

<li>I'm doing font-ish configuration of Emacs now and am amazed at how
retarded the font handling is from a user's point of
view. Technically, I'm sure it's wonderful, but it feels like I've
gone back two decades or something. How do I browse the fonts I have?
<tt>xfontsel</tt>? You're kidding, right?</li>

<li>Our product doesn't yet work with Firefox 3 [2], nor does the
web-based VPN product, so I was happy to see I can install both 2 and
3 without a problem.</li>

<li>Another incompatibility is the Cisco VPN client. According to
<a href="http://www.blog.arun-prabha.com/2008/05/01/cisco-vpn-installation-issue-with-ubuntu-804-hardy-heron/">this</a> 

a more recent version works fine, but the one we have access to at
work doesn't. I'll bug IT about downloading a more recent one.</li>

<li>Weirdly, the base install didn't include headers and such from
libc, so my initial run through the normal battery of Perl modules
failed miserably as the ones with XS bombed with a 'cannot find
sys/foo.h' buried among a whole bunch of compile errors.</li>

<li>There's a newer version of <a href="http://do.davebsd.com/">Gnome-Do</a> 
for 8.04 than for 7.10, cool.</li>

<li>Hooray, Postgres 8.3 is supported!</li>

<li>Finally, I enabled some of the 'Advanced' desktop stuff and now have wobbly
stretchy windows, an Alt-Tab that displays screenshots, and probably
some more eye candy. Not sure if I'll keep it yet. Maybe just for the
Monday presentation :-)</li>

</ul>

<p>More boring impressions later...</p>

<hr />

<p>
[1] "I think" because crap Outlook doesn't show me all the responses
from forwarded meeting requests.
</p>

<p>
[2] Lack of Firefox 3 support isn't a big deal for our users, trust me.
</p>


