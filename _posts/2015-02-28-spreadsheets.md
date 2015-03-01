---
title: "Spreadsheets!"
tags: "spreadsheets usability"
layout: post
---

A recent [Planet Money episode]() did a brief history of the spreadsheet, using
as its base a 1984 Harper's article about 
[A Spreadsheet Way of Knowledge](https://medium.com/backchannel/a-spreadsheet-way-of-knowledge-8de60af7146e).
<sup id="spreadsheet-fnref:1"><a href="#spreadsheet-fn:1" rel="footnote">1</a></sup>
I think the podcast is a great intro to the history -- VisiCalc, Dan Bricklin,
people buying computers just to use it -- and gives some sense of how important
the spreadsheet was to the computer being accepted in every day
life. The contrasts between doing spreadsheets manually -- on paper! -- and on
the computer were so stark and dramatic that the typical arguments countering
technology adoption got swept away.

How stark? One of the seductive features of technology is its maleability. One
aspect of this is asking it "What if?" questions, and the speed at which you
can do this can fundamentally change how you think about problems and solutions.
<sup id="spreadsheet-fnref:2"><a href="#spreadsheet-fn:2" rel="footnote">2</a></sup>
Back in the day even a simple question -- for example, one they posed during
the show was something like "What happens if we make candy bars 5% 
smaller?" -- would take **days** to answer. Spreadsheets made it possible to
answer it immediately and then move on to the next question with that answer
fresh in your brain. So: **stark**.

And it so happens that I'm reading (again) 
[Close to the Machine](http://www.amazon.com/Close-Machine-Technophilia-its-Discontents-ebook/dp/B007FU83DY)
which has a great few pages (76-80) about the spreadsheet and its differences
to the Web. Ullman wrote the book in 1997: fairly early in the Web's life and
before a lot of the interactivity that we take for granted these days, but
nearly 20 years after the spreadsheet's introduction. But I think the
comparisons and her points continue to apply today.  Generally they fall into
examples of the tension between software for consumption and production.

First, there's how users interact with the technology:

> When I watch the users try the Internet, it slowly becomes clear to me that
> the Net represents the ultimate dumbing down of the computer. The users seem
> to believe that they are connected to some vast treasure trove -- all the
> knowledge of our times, an endless digitized compendium, some electronic
> library of Alexandria -- if only they could figure out how to search it
> properly. They sit and click, and look disconcertedly at the junk that comes
> back at them. Surely it must be their fault, they reason; surely if they just
> followed the right links, expressed their query more accurately, used another
> search tool, then pages and pages of interesting information would soon be
> theirs....
> 
> In front of a spreadsheet, however, their helplessness and confusion vanish.
> When users want to show me the sort of information they have been storing,
> they open elaborate, intricate spreadsheets full of lists and macros and
> mathematical formulas, links to databases, mail-merge programs, and word
> processors. They have, in effect, been programming.

A lot of programmers look down on spreadsheets. Particularly because a fairly
common programming task is turning a single-user spreadsheet into a multi-user
shared system.
<sup id="spreadsheet-fnref:3"><a href="#spreadsheet-fn:3" rel="footnote">3</a></sup>
This typically involves unwinding years of history and business
decisions codified in a spreadsheet's workings, a hard task in any medium. But
I think it's even more difficult because complex spreadsheets can be *foreign*
to developers: they're not laid out like a program that you can read serially,
the functionality has to be ferreted out piece by piece.

But spreadsheets are indeed programming. That fact that they're commonly
created by actual domain experts who are solving actual problems (vs creating
tools to help other people solve problems) should be reason enough to mine them
for gold.

Here's another way of looking at that question:

> The spreadsheet presumes nothing. It has no specific knowledge, no data, no
> steps it performs. What it offers instead is a complex vocabulary for
> expressing knowledge. It is, literally, a blank sheet of paper with a notion
> of columns and rows -- and everything held on that sheet is presumed to come
> not from the program but from the human user. In the relationship between
> human and computer that underlies the spreadsheet, the human is the
> repository of knowledge, the samrt agent, the active party. The user gives
> data its shape -- places it in columns and rows, expresses the complex
> relationships among those columns and rows -- and eventually turns data into
> more knowledge. It is the end user who creates information, who gives **form**
> to data, who **informs** the spreadsheet.

The blank-sheetness gets at the heart of programming. Spreadsheets model the
world, just like software does.

Finally, another contrast to carry us out:

> The spreadsheet is the program that all but created the personal computer.
> The spreadsheet and the word processor -- two tools empty of information, two
> little programs sitting patiently and passively for their human owners to put
> something interesting into them. Now, fifteen years later, the Internet
> browser is the program creating the second generation of the personal
> computer. the browser -- a click-click baby tool for searching the Web, where
> everything of interest already resides. It is a journey through the looking
> glass in the age of information: one pill makes you larger, and one pill
> makes you small.

If you haven't read her book I strongly recommend it. It's a collection of
essays, and a fairly slim one at that. Her book [The Bug](http://www.amazon.com/Bug-Ellen-Ullman-ebook/dp/B007FU8F28/)
is also a fun one. She's a wonderful evoker of many essences of software and
creating it.

<div class="footnotes">
<ol>
    <li class="footnote" id="spreadsheet-fn:1">
      <p>
        ...written by Steven Levy. It's pretty amazing how long he's not only been writing, but also writing with both insight and perspective.
        <a href="#spreadsheet-fnref:1" title="return to article"></a>
      </p>
    </li>
    <li class="footnote" id="spreadsheet-fn:2">
      <p>
        ...which is, of course, the driving motivation behind agile software
        practices. And the better we get at it the more questions we can ask -- about
        tools, practices, libraries, patterns, hardware, all the way down.
        <a href="#spreadsheet-fnref:2" title="return to article"></a>
      </p>
    </li>
    <li class="footnote" id="spreadsheet-fn:3">
      <p>
        shout out to my Summa friends 
        <a href="#spreadsheet-fnref:3" title="return to article"></a>
      </p>
    </li>
</ol></div>

