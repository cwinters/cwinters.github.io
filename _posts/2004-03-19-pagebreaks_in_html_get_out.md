---
tags: technology
layout: post
title: "Pagebreaks in HTML? Get out!"
---



<a href="http://www.javascriptkit.com/dhtmltutors/pagebreak.shtml">Specifying page breaks for  printing using CSS</a> - I'd heard of this before but never tried it. Seems to work with Safari, although not with the style attached to an <tt>IMG</tt> tag. Using it with a <tt>DIV</tt> seemed to work best. Here's an example where I've got four yahoo maps images, two per page:
<pre class="sourceCode">
&lt;div align="center"&gt;
  &lt;img src="map_4.jpg" /&gt;
  &lt;br clear="all" /&gt;
  &lt;img src="map_3.jpg" /&gt;
  &lt;br clear="all" /&gt;
&lt;/div&gt;
&lt;div align="center" style="page-break-before:always"&gt;
  &lt;img src="map_2.jpg" /&gt;
  &lt;br clear="all" /&gt;
  &lt;img src="map_1.jpg" /&gt;
&lt;/div&gt;
</pre>


