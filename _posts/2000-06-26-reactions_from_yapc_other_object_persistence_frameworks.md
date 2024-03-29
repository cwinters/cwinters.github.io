---
tags: perl
layout: post
title: "Reactions from YAPC, other object persistence frameworks"
---



Back at home now, at least for a few days. Barb and I went out to Indiana for the annual Winters family reunion. It was fun, but there was a cloud hanging over at least my immediate family because my grandmother is quite sick. She probably hasn't missed one of these reunions for 60 or more years and we all missed her.

<p>Driving to and from Indiana wasn't bad. Picked up a rental for the trip, since our current car isn't fit for long trips. It had this weird Autostick thing: you can use it like an automatic, or you can use it like a manual. Except there's no clutch, and the gearbox is poorly marked so if you don't look at the tiny digital display on the dash to tell you what gear you're in, you can be in <b>1</b>st gear when you think you're in <b>D</b>rive and get all confused. I fail to see the utility of this thing. As far as I can see, it only adds complexity to one area of the car which sorely doesn't need it, the transmission. (But then again, I know as much about cars as I know about indigenous Australian reptile life.)</p>

<p>The yapc conference was excellent, of course. Rusty <a href="http://www.kuro5hin.org/?op=displaystory&sid=2000/6/25/17247/1308">posted a story on k5</a> about it, and I'll probably put all my comments about the show there. That said, I met a few people who are doing object persistence work. Of course, we're all approaching it a little differently, but with the same basic goals. Alzabo is one which aims to be a complete data modelling tool. I think it's interesting and he's done a pile of really interesting work on it, but it seems to be focusing its energies in a direction which doesn't really take a lot of work as it stands right now. Issuing 'ALTER TABLE' statements is not that difficult, and trying to create a wrapper which deals with all the possibilities is (IMO) fraught with danger. But more power to him! If he can create a powerful schema manager that works reliably on lots of different SQL databases, that would be a killer app for Perl.</p>

<p>However, none of these schemes address two things I feel are important:</p>
<ul>
<li>I don't care where the data comes from (RDBMS, LDAP, NDS)</li>
<li>I want to have object-level security </li>
</ul>

<p>So SPOPS should have a nice little niche :)</p>

<p>I also learned about an object persistence mailing list, which is super-cool. There are a lot of brainiacs working on this right now, and if I can take advantage of their powers for good, so much the better. 


