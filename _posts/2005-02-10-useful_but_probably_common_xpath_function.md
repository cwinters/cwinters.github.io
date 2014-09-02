---
tags: java xml
layout: post
title: "Useful but probably common XPath function"
---



<p>I don't work with XML often enough to have this always at the ready, so: <tt>normalize-space()</tt> will take care of chomping sequences of whitespace to a single space. So when you're trying to match something like:</p>
<pre class="sourceCode">
&lt;p>This is my
Great Page Number Three
summary
&lt;/p>
</pre>

<p>You can just use something like this and it will do the right thing (using <a href="http://www.dom4j.org/">dom4j</a> if that matters):</p>
<pre class="sourceCode">
 String path = "//p[contains( normalize-space( text() ), 'This is my Great Page Number' )]";
 List matching = doc.selectNodes( path );
</pre>

<p>(...and when I say 'XPath function' I actually mean 'XSLT function also used by XPath'. But since I'm just using XPath right now...)</p>

<p><b>UPDATE</b>: There seems to be a bug with 'normalize-space' in the XPath engine (jaxen) shipped with dom4j -- sometimes I get a 'StringIndexOutOfBoundsException', sometimes I don't -- it might have to do with single-space strings (referenced as <a href="http://jira.codehaus.org/browse/JAXEN-22">JAXEN-22</a>), but I'm not sure. In any case, you can <a href="http://jaxen.org/cvs-usage.html">grab the code from CVS</a>, modify the ant 'jar' task to <b>not</b> depend on 'test' since one or more tests fail, run 'ant' and replace your jaxen jar with the newly built one. It's worked so far...</p>


