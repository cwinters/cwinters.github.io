---
tags: perl
layout: post
title: "Finally got to work on OpenInteract"
---



<p>I finally got some time this weekend to work on OpenInteract2 -- the fifth beta is very overdue as I'd hoped to get it out by the end of August. (But August was a hugely chaotic month...) Part of getting back into it was getting my codebase in sync with CVS since I'd made some changes and never committed them -- bad Chris! Another part was <a href="http://jira.openinteract.org/secure/IssueNavigator.jspa?reset=true&mode=hide&pid=10010&statusIds=5&statusIds=6&updatedPrevious=604800000&sorter/field=updated&sorter/order=DESC">closing a bunch of issues</a> that I could immediately deal with. Tonight I'll try to deal with some more and schedule the rest.

<p>It felt really comfortable to get back into coding Perl. I've been working heavily on a web scenario testing project in Java at work for the last couple of weeks, and it always surprises me that I can slip back into Perl and OI2 without too much effort even though I'm away for fairly extended periods of time (this time about 10 weeks now). One of the good side-effects is that I can switch hats much easier. So design decisions I made with my architect/coder hat that make my life with my implementation hat get fixed much more quickly. 

<p>For example, Actions in OI2 are observable. This means you can attach objects, subroutines or classes to another object to catch observations. These attached objects are probably more commonly known as listeners, but that has the connotation of objects with state rather than just pieces of code out there waiting to react. Granted, it's not much of a difference.

<p>One instance of an observation is 'filter' which all Actions fire off just before returning their content. To configure the filters you had a 'filter.ini' file -- where 'configure' means 'register' and 'map to action' -- and a base 'OI2::Filter' class. Easy to understand, no problem.

<p>But what happens when you want to register a non-filter observer? Oops. Everything still works but you'll be registering observers in a file called 'filter.ini' and with methods like 'add_filter_to_action()'. Very confusing. And it may be that I'd always intended to fix this but since I can't load the state of my brain as of nine months ago I don't know.

<p>So with my implementation hat on I changed all 'filter' references to 'observer', made the configuration file easier to understand and added shortcuts to make doing common tasks really easy and understandable. I also added a simple implementation of a filter to the distribution of questionable value -- it changes all text to upper-case -- just so users could have something to fiddle with and see that it actually works.

<p>Finally (and probably most importantly), I could do this because I had an actual reason to put on my implmentation hat -- catching a 'post add' observation and posting a <a href="http://use.perl.org/journal.pl?op=top">use.perl journal entry</a> from the object just created. This has been one of the most valuable lessons of experience -- I should never build something unless I have a reason to use it. Contrary to blogging traditions I won't generalize and say this is true for everyone, but for me it triggers latent massive tendencies for overengineering. Now to just do tests as I go...


