---
tags: presentation web
layout: post
title: "Why isn't there a website-in-a-file?"
---



<p>Maybe this is crazy talk, but it would be awfully nice for browsers to be able to resolve resource paths in archives like Java does in JAR files. For instance, I could create a presentation with something like <a href="http://meyerweb.com/eric/tools/s5/">S5</a> and zip up its directory structure into a single file -- 'mypresentation.zip'. That file would have all the HTML, CSS, JavaScript, images and whatever else I need to persuade someone that Triscuits are much better than Wheat Thins. (Or whatever.)

<p>Then I could send 'mypresentation.zip' to my Wheat-Thin-eating buddy Clyde who can open his browser, choose, 'File | Open...' and pick my file. (Or right-click, choose 'Open with...' and pick the browser, whatever.) And he'd be able to see my presentation no matter how many graphics, CSS files, JavaScript files it referenced. And Clyde wouldn't even know or care about all that; he'd just have an overwhelming urge for baked, whole-wheat crackers.</p>

<p>So the browser would be responsible for:</p>
<ol>
  <li>opening an archive file (format doesn't matter)</li>
  <li>opening the right file initially (name it 'index.html', 'home.html', 'Default.htm': whatever floats your boat),
  <li>resolving references within the archive as directory paths -- so if the root level 'index.html' used 'ui/slides.css' the browser would know how to find it.</li>
</ol>
<p>AFAIK it already knows how to do the first and third, and the second is just a matter of using what 99% of people already use today. Some judicious use of temp directories (which they're already doing, right?) and you're set.</p>

<p>This doesn't seem very difficult and I'm sure I'm not the first to think of it. Is there something like this now? (Besides PDF or PowerPoint...)</p>



