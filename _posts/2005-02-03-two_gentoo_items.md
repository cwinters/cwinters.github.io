---
tags: gentoo linux
layout: post
title: "Two gentoo items..."
---



<p>Item the first: maybe it's just my machine, but has anyone else noticed that updating the portage cache after doing an 'emerge sync' is taking way, way longer than it used to? By 'way, way' I mean: old way was 15 seconds, new way is 2 minutes.</p>

<p>Item the second: I just discovered the utility 'revdep-rebuild'. It describes itself as a 'Broken reverse dependency rebuilder'. What does this do? Say you upgrade the 'openmotif' package to whatever is newest, but the upgrade somehow breaks the packages that depend on it. (I'm not exactly sure how this happens -- naming changes? -- but it doesn't really matter.) So you issue this command and gentoo scans all the installed package dependencies, finds anything broken, and rebuilds them from source. Sweet!</p>


