---
layout: post
title: "Potential TWiki security hole"
---



<a href="http://twiki.org/cgi-bin/view/Codev/NoShellCharacterEscapingInFileAttachComment">TWiki bug explanation and patch</a> - Shell characters aren't escaped/filtered when checking in file attachments. Simple patch available on the TWiki site, and a good reminder of why you should <b>always</b> prefer the list form of the Perl <tt>system</tt> call over the string form.


