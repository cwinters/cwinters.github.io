---
tags: java
layout: post
title: "How do you build a GUI?"
---



I've been looking around at different tools to do development of a GUI and I'm probably more confused than when I started. (NB: I've never done GUI development -- HTML doesn't count -- so I could be talking out of my ass.) I'd like to use a standalone tool to create a GUI layout since we're using IDEA which doesn't have anything built-in. (Plus I think it's a bad idea to tie yourself to a particular environment/editor for something like this.)

<p>So: does anyone use one of the standalone tools to do build interfaces, or do folks doing GUI programming use an IDE that has this functionality built-in (NetBeans/Forte, JBuilder, etc.)? Or do you just build them by hand? It looks like an IDE with GUI builder tools will generate code and place your customizations inline, while the standalone tool will place the layout information in some format (XML, properties, who cares) and when that particular interface is needed you request it from a factory which reads the layout information and creates the interface with hooks to your code (listeners, etc.). I'm not sure if this happens via code generation at runtime, if you need to create the classes from the layout info or what. FWIW, along the way I found <a href="http://www.acooke.org/andrew/diary/2002/aug/18.html">an interesting post</a> by Andrew Cooke comparing a few different tools.</p>


