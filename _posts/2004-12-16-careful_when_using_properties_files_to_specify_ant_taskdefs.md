---
tags: java scm
layout: post
title: "Careful when using properties files to specify Ant taskdefs"
---



<p>This is so trivial that I'm hesitant to post it. But it might save someone a few minutes. Short version: be sure to end any external taskdef declarations in a properties file with newlines.</p>
 
<p>Long version:</p>
 
<p>When using custom Ant tasks you have the option of specifying the name and class of the task in the <tt>&lt;taskdef&gt;</tt> tag:</p>
<pre class="sourceCode">
&lt;taskdef name="mytask"
     classname="com.mydomain.MyTask"/>
</pre>
 
<p>You can then reference this task like any built-in Ant task:</p>
<pre class="sourceCode">
&lt;mytask myOption="foo" myOtherOption="${bar}" />
</pre>
 
<p>Easy enough. But there's another way to declare a task:</p>
<pre class="sourceCode">
&lt;taskdef resource="mytask.properties">
    &lt;classpath refid="some.classpath.ref" />
&lt;/taskdef>
</pre>
 
<p>The referenced properties file (<tt><b>mytask.properties</b></tt>) is a simple name-to-class mapping like you'd expect:</p>
<pre class="sourceCode">
# Ant automatically makes these tasks available
mytask    = com.mydomain.MyTask
othertask = com.mydomain.OtherTask
</pre>
 
<p>And when Ant reads this in it loads the referenced classea and makes taskdefs available under the given names. Very useful for building task libraries, and pretty simple. But if the last line does not end in a newline Ant will die with something like:</p>
<pre class="sourceCode">
BUILD FAILED
.../build.xml:84: The following error occurred while executing this line:
.../build.xml:123: taskdef class com.mydomain.MyTask   cannot be found
</pre>

<p>If you have any experience with Ant your first instinct will be to check your <tt>classpath</tt> reference, make sure you don't have any typos or pointers to out-of-date JARs, whatever. Resist that urge, and first make sure your properties file has at least one trailing newline. (Sidenote: One of my sayings is: "When dealing with hardware, 90% of the time the problem is the cables." So: "When dealing with Ant, 90% of the time the problem is the paths." Except this time.)</p>


