---
tags: programming
layout: post
title: "Complex builds"
---



<a href="http://www.freeroller.net/page/ericfj/20030318#html_head_head_body_i">Three Warning Signs Your Build May Be Too Complex</a> - Eric gives some good tips about complicated builds. I used to do the first of these, but most of the complicated issues went away when I moved the libraries into the project directory. Previously I'd required people to specify directories for each one, but the setup file (in this case a properties file located in a subdirectory of the user's home) grew longer and longer, with more and more for the user to configure, until it was intolerable. Once I moved the development libraries into the project hierarchy I controlled them and only needed the developer to specify external resources like the application server home directory.

<p>The build process is like everything else: simplicity is golden. Sometimes it's easy to forget that when you've spent a lot of time and effort on a particular process, mending it along the way without stepping back and taking in that the process has at some point become nothing but patchwork.</p>


