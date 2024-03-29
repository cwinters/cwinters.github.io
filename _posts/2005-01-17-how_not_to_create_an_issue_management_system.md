---
tags: badsoftware gui scm
layout: post
title: "How not to create an issue management system"
---

We're in the process of moving to a new issue management system at
work. Our old Access-based one was written in-house and is quite...
clunky. (I'm not supposed to say that because I'll step on someone's
toes. But if I write piece-of-shit software I'd rather someone tell me
so I can fix it rather than pretend everything is ok.)

Anyway, the new system is
<a href="http://www-306.ibm.com/software/awdtools/clearquest/">Rational ClearQuest</a>.[1]
We've gone through some sort of process to settle on this software with a
committee and meetings and such. (I'm sure information about it is on the
internal wiki but I'm not interested.) And our project is the pilot for it so
all our new issues will be entered into ClearQuest and hopefully our feedback
will help shape the future direction of the product.

As the pilot team we needed a demo and overview of the system and
late last week we got it. But keep in mind that in the best blogging
tradition I haven't actually **used** the system yet. My
opinions here are based on notes I took during the demo and conversations
we had during and after it.

**1.** The standard interface is a Win32 client rather than a web browser.
(This is almost a deal-breaker for me.) Plus, it looks like ass -- probably why
they don't have many screenshots on the website...

Apparently there's some sort of web portal but we didn't see that. According to
<a href="http://www3.software.ibm.com/ibmdl/pub/software/rational/web/datasheets/version6/clearcase.pdf">the datasheet</a>
CQ web access works with IE, Mozilla and Safari (!), so it might be okay but
given the state of the Win32 client I'm extremely skeptical. I'm also unsure
how much pain the IT department is willing to bear to deploy it, particularly
if it depends on WebSphere...

**2.** Searching is case-sensitive. So if you look for a project 'mercury' you
won't find 'Mercury'. Jesus, how can someone design something like that in this
day and age? (Another potential deal-breaker.)

**3.** There's no 'search' box. Instead you have to create a query (using
another awful interface) or reuse queries that you or someone else
have stored for later use. And there's no way to just jump to issue
number N without using queries. Again, another straw on the
deal-breaker camel's back.

**4.** The client doesn't seem to use standard Windows GUI controls. So you
can't type in dropdown boxes and quickly navigate the list of items. Since a
number of the dropdowns have tons of possible values navigation slows to a
crawl. I hate Windows applications anyway, so this just makes it even more
painful.

**5.** File attachments seem to be stored in the database rather than a
filesystem. And given typical BLOB issues we were given a general "don't use
too many attachments" warning. Yeah, it's not like people need that or
anything...

Much to the developers' surprise though, the Win32 client sent the file to the
right application when we asked it to 'Open' one of them.

**6.** There are a ton of labels that are obviously just slightly-cleaned
variable names, if not direct variables. (This may be a customization issue.)
So you'll see things like `Is_Issue_Foo_or_Bar` on a form or a
directive to change to the `To_investigation` state.

**7.** I don't think you can create a printable version of an issue or a query
without Crystal Reports installed. But I could be wrong about that.

**8.** There's no screen with all information about an issue in one place. Just a
dialog with about 10 tabs. While I guess tabs have been used to good effect
somewhere they're generally just terrible, especially when all the tabs deal
with different data attached to a single record.

**9.** There don't seem to be any shortcuts for commonly used data. For
instance, in a number of places you're asked to reference a product, and the
product includes version numbers so you'll have 'Mercury 1.00', 'Mercury 1.01',
'Mercury 1.02' as separate entries. Since many developers are working on the
next version of the software it would make a lot of sense to have a 'Mercury
LATEST' so you never even have to think about it.

**10.** The client exposes you to data and relationships you don't need to see.
This is a gigantic usability problem and IMO the problem with many user
interfaces because it makes the common case really hard. (All software should
subscribe to: "Make easy things easy and hard things possible.") There are so
many ways this manifested itself but I only jotted down a couple.

Here's one example: when entering an issue you have to create the issue (title,
description plus some additional data) and then associate it with one or more
"change requests". Your issue might touch several different products (or
versions) and each one of these gets a change request. Makes sense from a data
management standpoint, no problem. But the steps I have to take to create an
issue are (from memory):<

* enter a title and description
* click the tab for change requests (it's red, indicating it requires
  data)
* click 'Create' to create a new change request
* in the new window that pops up, fill in data to three or four
  tabs, one or two of which have the above-mentioned issues with
  dropdowns so it takes twice as long as it should
* click 'Apply', which closes the change request window
* click 'Apply' for the original issue since it's associated with
  the change request just created (even worse: if I click 'Cancel'
  here instead of 'Apply', the change request is now an orphan!)
 
Hey, I've got a great idea: I want people to enter solid issue
reports so I can fix and improve my software the best way possible. So
I'll create a system which drives them to absolute rage when they
enter issues!

More examples on this, just with identfiers:
  
* The IDs for issues and change requests look totally
  different. The former are fairly reasonable (like '2015' or
  something), but the latter are just awful, looking something like
  'vfDB0000007'. And that's <b>supposed</b> to be a user-facing
  number!
* The user sees a number of identifiers that don't mean
  anything. When viewing an issue record you're given the standard
  Access control at the bottom of the page to navigate
  backward/forward to other records, and an ID is displayed there. But
  it's really long (10 digits or so) and isn't used anywhere else.

Finally, one thing to keep in mind is that ClearQuest seems more like a toolkit
than a finished system and many of these problems might be fixed with further
customization. If they are I'd be happy to post about this again.

[1] Sorry <a href="http://www.atlassian.com/">Atlassian</a> folks: I would have
recommended JIRA in a heartbeat, but I had no say in this. One of the hazards
of working for a larger company is that you'll probably have less of a say in
the company-wide tools you use.
