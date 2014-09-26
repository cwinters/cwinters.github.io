---
title: "Mocha nested hook ordering"
layout: post
tags: javascript testing mocha
---

A short bit of searching didn't turn up a decent answer for this so I'll
put this here for later.

In [Mocha](http://visionmedia.github.io/mocha/) using
`before`/`beforeEach`/`after`/`afterEach` in nested `describe` blocks generally
work first-in first-run for 'before', and 'first-in last-run' for 'after'.

Here's an example, no libraries except Mocha needed -- I had version 1.21.4
installed. You can't rely on the ordering of A + B, I just labeled them so
they'd be distinguishable.

{% highlight javascript %}
'use strict';

describe('level 1', function() {
  before(function() { console.log("L1 - before") });
  beforeEach(function() { console.log("L1 - beforeEach") });
  after(function() { console.log("L1 - after") });
  afterEach(function() { console.log("L1 - afterEach") });

  it('L1 test A', function() {});
  it('L1 test B', function() {});

  describe('level 2', function() {
    before(function() { console.log("L2 - before") });
    beforeEach(function() { console.log("L2 - beforeEach") });
    after(function() { console.log("L2 - after") });
    afterEach(function() { console.log("L2 - afterEach") });

    it('L2 test A', function() {});
    it('L2 test B', function() {});
  });
});
{% endhighlight %}

Here's what you'll see:

      level 1
    L1 - before
    L1 - beforeEach
        ✓ L1 test A
    L1 - afterEach
    L1 - beforeEach
        ✓ L1 test B
    L1 - afterEach
        level 2
    L2 - before
    L1 - beforeEach
    L2 - beforeEach
          ✓ L2 test A
    L2 - afterEach
    L1 - afterEach
    L1 - beforeEach
    L2 - beforeEach
          ✓ L2 test B
    L2 - afterEach
    L1 - afterEach
    L2 - after
    L1 - after
    
      4 passing (5ms)

