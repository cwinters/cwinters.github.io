---
layout: post
title: "Emerging mailman on Gentoo"
---



Note to future self: when running <tt>emerge net-mail/mailman</tt> first go into the relevant <tt>.ebuild</tt> file and change the <tt>MAILGID</tt> to the group sendmail runs as (normally 'daemon', or '2') and the <tt>APACHEGID</tt> to the group apache runs under (normally 'apache' on Gentoo systems, but it's typically 'www' on my customized processes).


