---
layout: post
title: "One of those java features I should have known: class.isInstance()"
---



One of the few times I've written a piece of functionality and actually found it later: the <tt>isInstance()</tt> method of the <tt>Class</tt> class. It's useful when you're dealing with generic classes and therefore cannot use <tt>instanceof</tt>:

<pre class="sourceCode">
void ensureAllHaveParent( Collection c, Class parentClass ) {
    for ( Iterator it = c.iterator(); it.hasNext(); ) {
        Object o = it.next();
        if ( ! ( o instanceof parentClass ) ) ... // WRONG!
        if ( ! parentClass.isInstance( o ) )  ... // RIGHT!
    }
}
</pre>


