---
tags: java javascript scripting
layout: post
title: "How to create inner class-like implementations in Rhino"
---



<a href="http://mozilla.org/rhino/">Rhino</a>, the pure-Java JavaScript interpreter, has received fairly short shrift in the dynamic-languages-for-Java meme. Maybe this is because many people have a bad impression of JavaScript because of its browser associations? Who knows. But it's pretty darned nifty.

<p>In the Rhino documentation the "Implementing Java interfaces" section in <a href="http://www.mozilla.org/rhino/ScriptingJava.html">Scripting Java</a> talks about how it creates the equivalent of anonymous inner classes. Basically, you can create an anonymous JavaScript object that has a property 'foo' set to 'bar' like this:</p>

<pre class="sourceCode">
var myobject = { foo: "bar" };
</pre>

<p>It's anonymous because it has no class behind it. It's actually more like a plain old Perl hash than an object, and if memory serves the <a href="http://www.oreilly.com/catalog/jscript4/">Rhino book</a> refers to the JavaScript Object as a simple associative array. But in JavaScript, especially when using it with Java, it's simple to morph the Object into something else. (You can rebless a Perl object but it's frowned upon.)</p>

<p>Extending that, you can create an object with the anonymous method 'foo' that  returns 'bar' like this:</p>

<pre class="sourceCode">
var myobject = { foo: function () { return "bar" } };
</pre>

<p>Again, not so interesting. Adding a code reference to a Perl hash is standard stuff.</p>

<p>Here's the nifty part -- you can marry these anonymous JavaScript objects with Java interfaces. Say you had an interface 'Fooable':</p>

<pre class="sourceCode">
package com.foo;
public interface Fooable {
    public String foo();
}
</pre>

<p>You can create a JavaScript object that can be used by Java classes expecting a 'Fooable' object like this:</p>

<pre class="sourceCode">
importPackages( Packages.com.foo );
  
// create the JavaScript object and wrapper separately
var myobject = { foo: function () { return "bar" } };
var fooable = new Fooable( myobject );
  
// same thing, just all-in-one...
var fooable = new Fooable( { foo: function () { return "bar" } } );
</pre>

<p>From what I understand, behind the scenes Rhino creates a proxy that delegates all calls to the wrapped JavaScript object. (Technically this is using a 'JavaAdapter' object rather than a 'java.lang.reflect.Proxy' or something else, but I haven't looked into the details.) One difference between this and manipulating JavaScript prototypes is that you can't replace the methods later:</p>

<pre class="sourceCode">
importPackages( Packages.com.foo );
  
// fails, 'foo' not implemented!
var fooable = new Fooable();
  
// create placeholder for 'foo' works...
var fooable = new Fooable( { foo: function () {} } );
  
// ...but replacing it later fails!
fooable.foo = function () { return "bar" };
</pre>

<p>As a more complete example, here's some Rhino code to pick a random file from a directory, with an optional matching pattern to restrict the files to choose from. (I've chosen to maintain a Java-ish feel in how the 'FileFilter' is created so I don't alienate people on my team not as familiar with JavaScript.) Note that 'File' and 'FileFilter' are both Java classes from the 'java.io' package.</p>

<pre class="sourceCode">
importPackages( Packages.java.io );
  
function chooseRandomFile( dirName, filenamePattern ) {
    var dir = new File( dirName );
    if ( ! dir.isDirectory() ) {
        return null;
    }
    var matchingFiles = dir.listFiles( new FileFilter({
        accept: function ( file ) {
                    if ( ! filenamePattern ) {
                        return true;
                    }
                    var pattern = new RegExp( filenamePattern );
                    return pattern.test( file.name );
                }
    }) );
    return pickRandomItem( matchingFiles );
}
</pre>


