---
title: "Some impressions of 'Soul of a New Machine'"
layout: post
tags: "book technology hardware"
---

I had read this book sometime in the mid-80s to early 90s, and
remembered very little. It's the story of a semi-skunkworks project at
Data General in the late 1970s to build a 32-bit minicomputer,
primarily to respond to recent DEC VAX systems which were so popular
they had nine-month backorders.

The book makes reference to an internal struggle as to which team
would get to build Data General's response. The company had recently
built an engineering HQ in North Carolina, which caused a lot of
resentment in the Boston-area home office. (Yes, working in distributed
teams has always been hard.) The NC group won the battle to build the new
system, but Tom West was able to quietly finagle a different tactical line by
emphasizing backward-compatibility with their 16-bit Eclipse line, though they
had the mandate from the CEO (former engineer who started the company under
semi-suspicious circumstances) for "no mode bit".

The book goes into detail not only with different parts of computer
architecture -- ring security for multiuser systems, microcode, registers,
boolean logic and transistor gates, etc -- but it also focuses on a half-dozen
or so members of the team, manager and entry-level workers alike. notably:

- Tom West, the initiator
- Carl Alsing
- Steve Wallach, architect; one focus of his was to get something Out
  The Door and not work on another project that would never see the
  light of day. Kidder had a wonderful passage where he was describing
  how Wallach came up with the method for tagging memory blocks with
  the rings it was allowed to interact with -- the description of
  pounding your head on the wall (literally in this case) and then
  seeing the solution as plain as day rang so true.
- Ed Asala
- Josh Rosen, who came from another group where he was a superstar and
  found he was just a normal guy on this team; the go go get it done
  nature of the project rubbed on him, and he left before it
  completed. His leaving was presented as a failure by his manager to handle
  him right rather than a failure on his part, which I found very interesting
  and reminiscent of some of the systems + people thinking bubbling up from
  places like Etsy.
- Ken Holberger
- Jon Blau
- Rosemary Searle, secretary and "mom" of the group, which was kind of
  regrettable given the lack of female engineers.
- Guyer and Veres who come in later in the book and are a good
  demonstration of the back-and-forth of good collaboration, and also
  how people can do amazing compression of ideas and communication
  when they work with each other a long time.

Some things that struck me:

- Amazing writer. This is one of the best books I've read.
- Kidder was completely in it. While it might have been better in one
  sense to compare/contrast this team with the one in NC (which
  apparently never finished their project), he wouldn't have had the
  depth of detail and ease of discussion that he would have. His
  discussions of getting lost in Adventure, or debugging, or stewing
  on a problem for days only to come up with the solution in the
  shower were so spot on.
- The descriptions of the system cache and accelerator were incredible
  -- he built on discussion of machine instructions and went into just
  enough detail of these so you could see how much a problem debugging
  them was, and how much people had to go through when things didn't
  go correctly.
- Similarly, when he goes into how the microcode gets executed with
  ticks of a computer's clock: "Tick" (actions happen) "Tick" (more actions)
  "Tick" (more still) ... fantastic.
- In nearly every description of each person, especially the younger
  ones, they got started because their high school had an IBM machine,
  usually older. What does it mean today that computing is so
  ubiquitous? Is it that far more people who have the nature and
  proclivity will wind up in computers?
- I wonder what these guys would think of today's software
  development. It's so high level, but we can get just an incredible
  amount of actual work done. They'd probably be both horrified at how
  much inefficiency reigns and mystified at the speed and power of
  today's systems.
- This seemed to mark a span of time before which it was possible for
  one or two people to "know" a computer, and after which it
  wasn't. Multiple people struggle with it -- Tom West, who keeps
  threatening to debug the thing himself; Ed Asala, whose debugging
  approaches and schedules initially fall short but eventually work
  though sheer will- and person-power.
- The book mentions multiple times how rare female engineers
  are. Problem even then, it would have been nice to hear from the
  ones who were there though.

Notable passages:

(from Prologue, where he talking about a group of men taking a sailing
trip around New England)

> Most of the crew now fell into that half-autistic state that the
> monotony of storms at sea occasionally induces. You find a place
> to sit and getting a good hold of it, you try not to move
> again. The boat rolls this way and you flex again. Just staying in
> one place is exercise. For a while your mind may rebel: "Why did
> you come, idiot? You don't have to be out here." You may feel
> remorse for having cursed some part of life on land. After a time,
> though, phrases start falling from your memory -- snatches of song
> or prayer or nursery rhymes -- and you repeat them silently. A
> little shot of spray in the face, however, or an especially loud
> and dangerous-sounding thump from the hull, usually breaks the
> trance and puts you back at sea again. You feel like a lonely
> child. The ocean doesn't care about you. It makes your boat feel
> tiny. The oceans are great promoters of religion, or at least of
> humility -- but not in everyone.

(Wallach seeing the ring number scheme, pp. 80-81)

>  Although they are generally shy about claiming to have had one,
>  engineers often speak of "the golden moment" in order to describe
>  the feeling -- it comes rarely enough -- when the scales fall from
>  a designer's eyes and a problem's right solution is suddenly
>  there. The chief virtue of Wallach's scheme was its simplicity. It
>  would be relatively cheap and easy to implement in hardware and
>  software, and it should work efficiently and reliably. When Alsing
>  saw Wallach's brief description of the plan he said to Wallach,
>  "That's nice." Later, out of Wallach's earshot, he said
>  more. "Rings have been around. They're old hat. What makes Wallach
>  a good Data General engineer is that he came up with a really
>  elegant subset of those ideas -- simple, sweet, cheap, efficient,
>  clean. And I can't believe I just said that about Wallach."
> 
> ... The idea of placing that neat, clean structure on top of the
> outdated structure of the Eclipse repelled him. It was as if he had
> invented a particularly nice kind of arch for the doorway of a
> supermarket.

(reviews and moving fast, pp 119-120)

> West reviewed all of the designs. Sometimes he slashed out
> features that the designers felt were useful and nice. He seemed
> consistently to underestimate the subtlety of what they were
> trying to do. All that a junior designer was likely to hear from
> him was "It's right," "It's wrong," or "No, there isn't time."
> 
> To some the design reviews seemed harsh and arbitrary and often
> technically shortsighted. Later on, though, one Hardy Boy would
> concede that the managers had probably known something he hadn't
> yet learned: that there's no such thing as a perfect design. Most
> experienced computer engineers I talked to agreed that absorbing
> this simple lesson constitutes the first step in learning how to
> get machines out the door. Often, they said, it is the most
> talented engineers who have the hardest time learning when to stop
> striving for perfection.

No grand sum-up, just that you really should read this book if you haven't
already. And even if you have it seems the sort of work that rewards your
accumulation of experience by making available new insights from the same text.

