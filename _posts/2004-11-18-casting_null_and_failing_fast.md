---
tags: java
layout: post
title: "Casting null and failing fast"
---



<p>I never thought about it before, but it turns out you can cast <tt>null</tt> with no ill effects. Here's an example:</p>
<pre class="sourceCode">
public class CastNull {
    public static void main( String[] args ) {
        Object someNull = null;
        String castedFromObject = (String)someNull;
        try {
            out( "Length: " + castedFromObject.length() );
        } catch ( NullPointerException e ) {
            out( "Caught NPE from castedFromObject" );
        }
        String castedFromNull = (String)null;
        try {
            out( "Length: " + castedFromNull.length() );
        } catch ( NullPointerException e ) {
            out( "Caught NPE from castedFromNull" );
        }
    }
    private static void out( String msg ) {
        System.out.println( msg );
    }
}
</pre>
<p>I had expected this to die at the two <tt>String</tt> casts. Nope. Each dies when you try to call a method on it -- this will print out both of the 'Caught NPE' lines from the <tt>catch</tt> blocks. If you think about <tt>null</tt> as an instance of <tt>Object</tt> (which happens to be null) then it makes sense, but doesn't the fail-fast principle tell us we should instead die at the cast?</p>


