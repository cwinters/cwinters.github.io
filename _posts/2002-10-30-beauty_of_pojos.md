---
tags: java
layout: post
title: "Beauty of POJOs"
---



<a href="http://radio.weblogs.com/0112098/2002/10/30.html#a217">Being architecture neutral</a> - I totally agree with James on his points. Back when I was <a href="/2002/09/25/strong_or_candidate_hibernate.html">looking at persistence frameworks</a> I came to the conclusion that submitting my domain objects to some sort of persistence manager was the way to go. Two main reasons why, both really stemming from simplicity:

<p><ul>
 <li>Testing: I can test object behavior without dealing with the database. This is crucial.</li>
 <li>Education: Teaching other people about the pieces of the system is now much easier. There are no Data Transfer Objects -- the object you use on the server in a Session Bean is the same as the object you use in a Servlet.</li>
</ul>

<p>This also allows me to create the processes as POJOs for testing purposes. So a Session Bean (or any other sort of coordinating component) just has to deal with transaction management and building the process objects. It's so crazy, it just might work!</p>


