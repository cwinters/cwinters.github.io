---
tags: opensource rest work
layout: post
title: "Work + open source: getting the point"
---



<p>At work I've been working on rearchitecting a server platform for <a href="http://healthcare.vocollect.com/global/web/us/solutions">AccuNurse</a>. And as I <a href="http://www.cwinters.com/news/display/3502">wrote before</a> I think <a href="http://rest.blueoxen.net/cgi-bin/wiki.pl">REST</a> offers a really useful way to let our systems and external systems interact with our data.</p>

<p>While there are <a href="http://java.sun.com/developer/technicalArticles/WebServices/restful/">layers</a> that sit on top of existing platforms to allow you develop "RESTfully", there are also projects that are built from the ground-up with the REST architectural style in mind.</p>

<p>AFAICT the main REST platform in Java is <a href="http://www.restlet.org/">Restlet</a>. It can run on top of Jetty (5 or 6), the Simple web framework, Async web, or in a servlet container. And while it's currently at 1.0 beta 18 the API still undergoes fairly substantial changes from release to release.</p>

<p>One of the (IMO) glaring omissions is the presence of a sample application that actually does something, even something trivial. The docs talk about how to get the server configured and running, but not so much about how you use the different types of objects to do work.</p>

<p>So I built one, which you can grab from <a href="http://www.cwinters.com/raw/RestSampleBook.zip">here</a>. And I submitted some minor documentation and code patches. And only then did I think that I should clarify what Vocollect's policy on working on opensource for work purposes. We do have a policy that you can work on opensource software in your own time, as long as it doesn't duplicate what you do at your job. But not what you do on the job.</p>

<p>So I posed the question up the chain. And the answer I got back was very gratifying. Paraphrased, it was: "We have as part of our business plan to lower costs by using open source operating systems and platforms. Part of using open source means participating in the process, which means giving back. So as long as it doesn't take too much time and it's appropriate to work, go ahead."</p>

<p>Good stuff.</p>


