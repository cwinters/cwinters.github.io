---
tags: java
layout: post
title: "More code generation articles"
---



<a href="http://www2.theserverside.com/resources/article.jsp?l=MDA">MDA from a Developer's Perspective</a> and <a href="http://www.zanthan.com/itymbi/archives/000884.html#000884">Alex's comments</a> on it. I can't emphasize enough that you should never modify generated code. But instead of Alex's subclassing approach, I tend to have customizations as an abstract parent of the generated code. When the code is generated it checks to see if there is customization class out there and if so extends that class. That way the user of the object never needs to know whether the item is generated or not and everything is named consistently.


