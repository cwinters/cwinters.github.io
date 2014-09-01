---
layout: post
title: "XEmacs modes broken after upgrade"
---



I recently upgraded gcc and glibc -- why? they were there... dumb -- and noticed some odd behavior in my XEmacs after doing so. It would edit files without a mode ('Fundamental') just fine. But once I invoked one by opening a known file type (e.g., cperl-mode for a .pm file) or by starting up PCL-CVS, the app froze with an 'X_OpenFont' error indicating 'BadValue (integer parameter out of range for operation)'. Wacky.

<p>Moving to a new WM fixed it, but then I figured to just give recompiling the previous WM (Sawfish) a try, plus its immediate libraries (the rep stuff). Fortunately since I'm using gentoo this was a matter of:

<p><pre class="sourceCode">
# emerge x11-libs/rep-gtk dev-libs/librep x11-wm/sawfish
</pre>

<p>Worked like a charm. Lots of perl coding ensues...</p>


