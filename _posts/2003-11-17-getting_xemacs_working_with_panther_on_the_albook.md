---
tags: programming
layout: post
title: "Getting XEmacs working with Panther on the AlBook"
---



None of this is rocket science, but since I didn't see a page with all this information in once place I figure it can't hurt. I assume they're mostly applicable to (Power|e|i)Macs as well, but I can't say for sure.

<p>I realize there are a number of native emacs implemenations out there. And I installed one. But I have a couple of reasons for using the XEmacs under X implementation. One reason: I've been using XEmacs for six or seven years and while I don't do a lot of customizations there are a few. A second: a native implementation won't read my SSH agent environment variables so I can use CVS seamlessly. Maybe there are other ways to get around this, but you can go somewhere else to find them.</p>

<p>Okay, onto business. First, install <a href="http://fink.sourceforge.net/">Fink</a>. The <a href="http://fink.sourceforge.net/doc/bundled/install.php">installation instructions</a> are very good (as is the other documentation I've read) and I've been content to use <tt>fink</tt> to compile everything rather than <tt>apt-get</tt> and company.

<p>If your PowerBook was shipped with Panther you probably need to go grab Apple's <a href="http://www.apple.com/macosx/features/x11/">X11 implementation</a> and install it. While you're at it you'll need to go into <tt>/Applications/Installers/Developer&nbsp;Tools</tt> and install the X11 SDK. You might as well install other dev tools while you're there, these things ship with big enough hard drives...</p>

<p>Now do a:</p>
<pre class="sourceCode">fink install xemacs</pre>

<p>It'll ask you to install a whole bunch of supporting libraries, just say yes. Then go grab a sandwich and a few chapters of your favorite book -- short chapters are okay. Hopefully it will compile cleanly. Once it does run:</p>
<pre class="sourceCode">fink install xemacs-sumo-pkg</pre>

<p>This brings in <b>all</b> the xemacs packages -- why not?</p>

<p>When you startup XEmacs you'll eventually notice that there's no Alt/Meta key. (I don't know the difference between these, nor do I care.) Even though the 'Option' key also has a small 'Alt' label it won't work. Instead you'll have to use 'Esc'. That blows. So here's how to change your key mapping so that the Command (a.k.a, 'Open Apple') key is used as the meta key.</p>

<p>Open up the file <tt>~/.Xmodmap</tt> and  enter the following:</p>
<pre class="sourceCode">
! Make 'Option' key be Meta and Command be Alt.
! See http://mail.gnu.org/archive/html/help-gnu-emacs/2003-05/msg00389.html
clear mod4
keycode 66 = Meta_L
keycode 63 = Mode_switch
add mod4 = Meta_L
</pre>

<p>Before shutting down X11 to reload this you'll need to modify a couple of options. Open up the X11 preferences ('X11 | Preferences...') and pick the 'Input' tab. (Are they called 'tabs' in Aqua? Whatever.) Uncheck the 'Follow system keyboard layout' and 'Enable key equivalents under X11'. Yes, this means that 'Command-,' won't open up your preferences window anymore, and you can't use 'Command-Q' to exit X. Oh well. You probably won't be shutting it down often anyway.</p>

<p>Now shutdown X and restart it, then fire up XEmacs. You should be able to use both Command keys as Meta/Alt, even with chords like Command-Q. Have fun.</p>

<p>There's probably something I've missed, an easier way to do something, etc. Let me know, I'm just learning...</p>

<p><b>UPDATE</b>: fixed comments in Xmodmap thanks to a comment.</p>


