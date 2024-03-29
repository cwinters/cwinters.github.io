---
tags: oi2 refactoring
layout: post
title: "Rethinking some core OI2 packaging and distribution assumptions"
---



<p>I've been working a lot recently on making OpenInteract2 more
standard -- 'standard' meaning you can install without having extra
directories around and that the applications are just CPAN
packages. This is a long-winded discussion of the issues and the
process that's led me to a very different view of the subject.</p>

<p>One of OpenInteract's strengths has always been that you can
package and distribution applications very easily -- a command from
the command-line tool 'oi2_manage' will create a new package for you,
another will turn it into a zip file, and other will install that zip
file to a website.</p>

<p>This is nifty, but the problem is that we have to create our own
distribution infrastructure because CPAN isn't built to handle such
files. And since there has been no effort to ever do so it's a pretty
safe bet there never will be.</p>

<p>For a long time I didn't believe these issues were a big
deal. (Actually, I thought about them very little. Too busy
implementing. Lame.) The motivations for creating distributable
packages in their current form came from a different set of needs. But
in thinking more about these and about how usability affects adoption
I've changed my opinion. This wasn't done overnight. At first I just
wanted a way for people to install OI2 without a 'source directory'. A
little background -- with the current CPAN version and and earlier you
need to do something like this to install OI2 from CPAN, create a
website and create a package for development:</p>

<pre class="sourceCode">
 # standard Perl module stuff...
 tar -zxvf OpenInteract-1.99_05.tar.gz
 cd OpenInteract-1.99_05
 perl Makefile.PL
 make
 make test
 make install
 # now we get into the customizations; 'source_dir' is the default here:
 oi2_manage create_website --website_dir=/path/to/site
 
 # if you're creating a website later, you need:
 oi2_manage create_website --website_dir=/path/to/site --source_dir=/path/to/oi2-source
 
 # if you're developing a new package:
 oi2_manage create_package --package=myapp --source_dir=/path/to/oi2-source
</pre>

<p>The 'source_dir' held two directories, 'sample' and 'pkg'. The
'pkg' directory held a set of zip files for the core OI2 applications,
and the 'sample' directory all the templated configuration and other
files for creating a new package and website.</p>

<p>Later I added a management task to create this source directory in
a public place ('/usr/local/oi2' or something), but that was just a
band-aid. I didn't think much about this just because there were so
many resources -- 110 files or so -- and, to be honest, I wasn't
really thinking from a user's point of view./p>

<p>So recently I had the idea to get rid of this source directory (see
<a href="http://jira.openinteract.org/browse/OIN-121">OIN-121</a> for
more). My first thought was to use 
<a href="http://search.cpan.org/dist/Inline-Files/">Inline::Files</a> and
treat all of those 110 resources as a file within a class. But I had
an odd problem with that (something about a scalar not being
promotable) and in the course of investigating decided it would be
easier to just make every resource a subroutine that returned the
contents of a heredoc.</p>

<p>After some (surprisingly small) reworking of the tools that
manipulated those 110 resource files that worked reasonably well. Then
I had to do the packages -- a set of zip files distributed with the
OI2 CPAN package. I figured I could use the same process but just
base-64 the zip contents and inline them the same way. And it worked!
We'd now rid ourselves of the hated source directory!</p>

<p>As I was doing that I remembered another issue (<a
href="http://jira.openinteract.org/browse/OIN-72">OIN-72</a>) about
making OI2 packages distributable on CPAN. I figured it would be just as easy
to use this same process to distribute a package. And it wasn't that
difficult, but it opened a whole slew of opportunities I didn't
foresee that forced me to rethink what a 'package' actually is.</p>

<p>First, some more background. A package is a full application,
consisting of:</p>
<ul>
  <li>Perl modules for actions, supporting classes, and declarations
  for installing your SQL structures</li>
  <li>Templates used to generate your content</li>
  <li>Web resources (html pages, images, etc.)</li>
  <li>Configuration for content-generating actions and
  object-relational mapping</li>
  <li>SQL data definitions for tables, sequences, whatever else you
  need</li>
  <li>Any initial data you want stored when your application is
  installed, including security settings</li>
  <li>Documentation</li>
</ul>

<p>OI2 has tools for installing a package to a website, creating its
SQL structures to a supported database (there are quite a few) and
initializing them with initial data.</p>

<p>CPAN doesn't care about any of these pieces except the first and
last items. It also cares about some metadata like authorship, what
other modules yours depends on, the license you're using, etc. What
that means is that we don't have to put them in some CPAN-compatible
format. All we have to do is bundle <b>those</b> resources into some
way that we can find them whenever we're installing the package.</p>

<p>So I created a management task for bundling an existing application
into a CPAN distribution, generating the necessary supporting files
like Makefile.PL, and creating an uploadable tarball. Works great.</p>

<p>But that got me thinking: why do we even need zip packages any
more? Instead of thinking about CPAN distributions as an alternate way
for packaging applications, why not think of them as <b>the</b> way?
Not only do they make a number of things easier, but they also get rid
of a longstanding problem we had when at startup we copied all the
package modules to a single directory called the 'temporary lib dir'
since we add it to @INC -- some people stored their directories on NFS
mounts and recreating this directory and copying all the files there
took quite a few seconds.</p>

<p>Since the modules would be installed to the normal @INC: no
problem. And since we're using a standard tool with support for
copying modules to a specific location, we can just give it a 'LIB' to
ensure that one website's packages don't get in the way of
another's. (This was one of the motivations behind packages, but from
what I've heard in practice few people use more than one OI
application per web server.)</p>

<p>


