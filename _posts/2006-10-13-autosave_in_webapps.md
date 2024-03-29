---
tags: usability web
layout: post
title: "Autosave in webapps"
---



<p>Auto save is implemented in lots of desktop applications. It's just the idea that every so often (seconds or minutes) the applications will store your work someplace safe, and you can get it back if the application crashes, or if you accidentally close it and click through the multiple 'Are you sure?' dialogs.</p>

<p>But what if you didn't even have a 'Save' option -- why do you even have to manage that? Isn't that why we have computers? Why can't the computer automatically store every change so that you never have to think about it? It's not so far out: Quicken has done this for a long time. It has the benefit of clearly demarcated transactions, but that's just a convenience.</p>

<p>But AFAIK autosave isn't seen so often in webapps. Entire frameworks are built up around translating the bag of text you get when the user clicks the 'Save' button into usable data (e.g., using an actual date object instead of '2006-10-05' or 'next Tuesday'). And the frameworks themselves are typically record- or object-centric, presenting a data record as a consistent, whole item so it can be mapped (with hopefully a minimum of dissonance) onto an HTML form.</p>

<p>What would happen if a webapp dealt with the individual pieces of data, rather than entire records? So if you check a checkbox, we send a message to the server saying, "activate the data element represented by the checkbox"; if you type in a person's name and tab to the next item, we send the name to be updated. If you figure out halfway through your edits that you're editing the wrong record you can just click 'Undo' and it'll roll back your changes since you loaded the form.</p>

<p>Since we're treating the web form as an active data editor we can remove concerns like validation from the browser. And treating data items individually would likely make it easier to create components to handle most of the work for you.</p>

<p>There are certainly problems with the approach. It means you have to version individual fields, which can be an interesting data management problem. (This also has a positive effect: stale-data conflicts become much more granular and easily resolved.) Some pieces of data are combinations of fields which may not make sense (logically or transactionally) to update independently, which means more things to manage. Managing 'Undo' functionality adds complexity as well. And a low-latency, always-on data connection between the browser and server is a requirement -- in fact, it might only work for intranet-type applications.</p>

<p>It's an interesting idea; while I'm not sure it's practical, it's a pretty good usability goal to shoot for.</p>


