---
tags: technology
layout: post
title: "Remembering why I don't like hardware..."
---



As I <a href="/2004/02/16/buying_a_new_server_for_openinteract.html">mentioned</a> a few days ago I put out a call for some help with purchasing a rackmount server to host the OI websites, demo websites, CVS, downloads, etc. I only received <a href="http://openinteract.sourceforge.net/cgi-bin/twiki/view/OI/OpenInteractDonations">two responses</a> so far (many, many thanks) but they were more than enough to make up the difference for the following:

<p><ul>
  <li>AOpen <a href="http://english.aopen.com.tw/products/server/baresystem/ft9100.htm">Fortress 9100</a>: AOpen DX3R-1U motherboard with dual P3, onboard SCSI, 1U case with hotplug mounts, case fans, CPU fans, CD-ROM + FDD and all that; also a set of rails (both from a <a href="http://cgi6.ebay.com/ws/eBayISAPI.dll?ViewSellersOtherItems&userid=stallardtechnologies-inc&include=0&since=-1&sort=3&rows=50">reputable ebay dealer</a>)</li>
 <li>512 MB registered ECC PC 133 from <a href="http://www.memoryx.net/aopenxar512.html">MemoryX</a></li>
 <li>2 P3 600EB FC-PGA CPUs from <a href="http://www.starmicro.net/detail.aspx?ID=82">Star Micro</a></li>
</ul>

<p>And unless some SCSI drives fall from heaven I'll just put my own in there, making this a pretty decent machine. Hopefully everything will come this week so I can have a couple weeks to install + test before taking it to its home in DC.</p>

<p>That's all mildly interesting, but here's the thing. I was prepared to wait a couple more weeks to see if any more Paypal money would float in. But once I started doing more research I really got sucked in. Really, really sucked in. Like "missing most of the first beautiful weekend in months" sucked in.</p>

<p>I think it's partly that there's so much stuff out there. You don't just go to The Server Dealer and choose from Columns A through G to get your machine. The only real things I knew going in were my budget (~$500) and that I needed a 1U or 2U machine. (I tended toward the 1U just in case my hosting arrangement doesn't work out, or they move, or whatever -- 1U machines seem like they're easier/cheaper to colo.)</p>

<p>Plus this whole rackmount thing is new to me. What distinguishes good cases from bad? (Besides bare metal that cuts your hands to shreds...) Does any ATX motherboard fit in any case? Do I need special cables? What are these riser cards good for? Does <a href="http://groups.google.com/groups?dq=&hl=en&lr=&ie=UTF-8&c2coff=1&threadm=1043b9te34r5683%40corp.supernews.com&rnum=1&prev=/groups%3Fdq%3D%26hl%3Den%26lr%3D%26ie%3DUTF-8%26group%3Dalt.comp.periphs.mainboard.tyan%26c2coff%3D1%26selm%3D1043b9te34r5683%2540corp.supernews.com">any riser card</a> fit in any board? How do the machines fit on the racks anyway -- some have rails, some don't...?</p>

<p>First you need to break down your requirements -- do you need dual CPUs (good for dynamic websites with the database and web server on the same machine)? Do you need fast CPUs? Do you need SCSI? Do you need hotplug SCSI? These aren't so hard but there are tradeoffs among them -- maybe SCSI isn't necessary if you have faster dual CPUs? Maybe if you have SCSI you only need a single CPU? Or slower dual CPUs?</p>

<p>So keep all that in mind you search around. After trawling a few rackmount factories and finding that my budget would likely dictate used and/or older equipment I went to ebay. There's a ton of stuff there, especially if you know what you're looking for. But I didn't know what I was looking for.... and that's a problem because you need to learn the parameters of the hardware to be able to separate (technically or financially) the wheat from the chaff. So you have PC2700 memory cheaper than PC133 just because it's more prevalent, but the boards using PC2700 are more expensive, as are the CPUs they take. Most P3 server boards take <b>registered</b> PC100/133 DIMMs (oh yeah, make sure to coordinate the memory with the CPU bus speed because servers are picky) but the L440GX can take either registered or unregistered (but don't mix) while the Supermicro and Tyan boards seem to be exclusively registered (some in pairs, some not) and the AOpen one requires registered too. But do they all use the <b>same</b> registered memory? Ah, AOpen says the board likes these particular Infineon and Samsung chips...</p>

<p>Quickly you get into the craziest minutiae that you need to keep ready while you're reading these listings, some of which contain the bare minimum of information (why? are they hiding something or are they just ignorant/don't care?) so you have to decide if they're reputable enough to bother asking them a question like what stepping is the single CPU in the dual-capable board because you want to see if another one like it is available at a decent price. (What's that? Stepping? Intel says that it matters but you don't need to match those five-character IDs; others seem to disagree. More minutiae....)</p>

<p>Anyway, after far too many hours of this paralysis masquerading as information gathering I decided that getting something unused would make the most sense, particularly since the machine is going to be four hours away. So to head off any more time wasted I just went ahead and got it. Hopefully it'll make its way online in a few weeks or so.</p>

<p>I look at this as another sign of getting older - when I was young I wouldn't mind spending so many hours performing hardware research, most of which would probably wind up meaningless. Now I just want to get the shit done...</p>


