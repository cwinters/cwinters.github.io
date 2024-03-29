---
tags: perl
layout: post
title: "Module::Build"
---



If you develop in Perl you should probably be aware of <tt>Module::Build</tt>. It aims to be a replacement for the venerable <tt>ExtUtils::MakeMaker</tt>, which is what generates the <tt>Makefile</tt> whenever you run <tt>perl Makefile.PL</tt> as the first step of a module installation process. Then you run <tt>make</tt> or one of its equivalents to actually do the installation. It also works with the CPAN shell to automatically fetch and install dependencies, plus run test suites for all modules installed. It is the envy of many other languages.

<p>While this is an amazing feat (<tt>EU::MM</tt> runs on almost as many platforms as Perl, which is huge), it points out an unfortunate problem: installing Perl modules requires a working <tt>make</tt>. Unixfolk take it for granted, but while a working equivalent (<tt>nmake</tt>) is available for Win32, it's another hoop to jump through. If you know what you're doing it's easy to get around, but most people don't -- they just want things to work.</p>

<p>Enter <tt>Module::Build</tt>, which replaces most of the functionality of <tt>EU::MM</tt> while being a pure-Perl module. So it will install Perl modules anywhere perl runs, which should be the whole point anyway. The build process looks almost exactly the same as it does now -- substitute <tt>./Build</tt> for <tt>make</tt> -- and extending seems to be much easier than extending MakeMaker.</p>

<p>I'm interested in it because in the next couple of months I'm going to need to update the testing and installation process for OpenInteract 2. OI 1.x has no testing at all (for shame!), SPOPS does, and modifying the process for it was a royal pain -- find out what DBMS/database name/username/password to test against, find out what LDAP server/cn root/dn/dn password to test against, etc. Ugh. And that's easy! Testing OI2 will require us to create a website installation (create a server configuration with smart default values, find all the packages install them to the website), fire up a standalone web server on a particular port, execute commands against it, stop the server, etc. (I know there's an <a href="http://perl.apache.org/docs/general/testing/testing.html">Apache::Test framework</a>, but work with me here.) Much more complicated. But because I can do everything in Perl it shouldn't be too much of a pain.</p>

<p>It's also an interesting process to watch because it (along with the CPANPLUS shell) is replacing one of the core pieces of infrastructure for what makes Perl so great use -- CPAN and the ease of installing modules from authors around the world. You'd think this would be a difficult process with sniping at all sides that M::B doesn't yet implement this esoteric feature, therefore it sucks! But that doesn't seem to be happening, partially because everyone recognizes the kludges necessary for MakeMaker and partially because the process is moving along steadily and openly.</p>

<p>Other resources:</p>

<p><ul>
  <li>Dave Rolsky published <a href="http://www.perl.com/pub/a/2003/02/12/module1.html">Module::Build</a> on perl.com a month and a half ago, which gives an excellent summary of the problems with MakeMaker and how much easier it is to extend M::B.</li> 
  <li>Schwern put together a <a href="http://magnonel.guild.net/~schwern/talks/MakeMaker_Is_DOOMED/slides/">set of slides</a> titled "MakeMaker is DOOMED!"</li>
  <li>M::B has a <a href="http://sourceforge.net/projects/module-build/">SF project</a> with a useful <a href="http://sourceforge.net/mail/?group_id=45731">mailing list</a></li>
  <li>More about <a href="http://www.perl.com/pub/a/2002/03/26/cpanplus.html">CPANPLUS</a> from a perl.com article by Jos Boumans</a></li>
</ul>


