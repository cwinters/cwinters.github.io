---
tags: qcon conference scalability design opensource
layout: post
title: "QCon 2009: unibet.com Architecture"
---



<p><strong>Stefan Norberg</strong></p>

<p>Open source software and standards should always be our first
choice.</p>

<p>Commercial s/w only chosen when there's <em>exceptional business
value</em></p>

<p>Contribute to the community by buying support, or by sponsoring
initiatives to improve the product.</p>

<p>(image with the architecture: pieces they use: Terracota, Esper,
protobuf, RabbitMQ, AcitveMQ)</p>

<p>unibet.com</p>

<ul>
<li>sports betting</li>
<li>online since 1998 </li>
<li>30+ sites in 27 languages</li>
<li>make about $250m/year</li>
<li>"technical" growth is > 100%/year</li>
</ul>

<p>2006 -- 80% of your customers will think about going elsewhere if
your page view time is 4 seconds; 2009: 2 seconds</p>

<p>How to do this?</p>

<ul>
<li>Latency: data too far away from where it's needed</li>
<li>Bottlenecks: resource contention</li>
</ul>

<p>Introduce Kevin:</p>

<ul>
<li>customer to candy store; wants to buy 40 pieces 
(including candy bars and bubblegum))</li>
<li>extremely small pockets; fit only one piece of candy</li>
<li>his house is very far from the store</li>
</ul>

<p>How to fix?</p>

<ol>
<li>Sell bags of candy! (But bag doesn't hold candy bar and
bubblegum)
<ul>
<li>Kevin is browser; bag of candy is one big JS file, or CSS
file </li>
</ul></li>
<li>Sell bags on street corners! (closer to user)</li>
</ol>

<p>But... data center is on a little island in Mediterranean
(Malta), for legal reasons. This is bad: poor roundtrip times,
etc.</p>

<p>Tune tune tune the front end. 
* 80/90% of end-user response time is spent downloading and
  processing all the components on the page.
* Rewrote and optimized all the front-end code -- spent 4 months
  on this, cut load time in half
* Implemented image spriting and fixed other issues w/cache
  headers
* best practices: Use YSlow and Page Speed
* progressive rendering key
* improve performance by having objects served close to user</p>

<p>http://www.webpagetest.org/ = be able to time how long it takes
to load a page</p>

<ul>
<li>Be close to users with CDN</li>
<li>Prepend CDN proxy name to all static files</li>
<li>Set a one-year cache time (no 304) (if more than year you'll be
marked as suspect)</li>
<li>Version static content</li>
<li>Stripe objects over several CNAMEs</li>
<li>Use several CDN vendors for load balancing, redundancy</li>
</ul>

<p>Live betting data distribution</p>

<ul>
<li>10000s of realtime clients need price updates almost every
second</li>
<li>20 concurrent games</li>
<li>10+ offers within one game</li>
<li>Product growth 60-80% per year</li>
<li>Right now, clients running bets are all hitting a single place
("like a laser beam attack on Malta")</li>
<li>Would rather have fan-out servers; working on this right now,
will go-live before Christmas
<ul>
<li>RabbitMQ, end-to-end messaging (referenced AMQP as "TCP/IP
for messaging)</li>
<li>Kaazing Enterprise Gateway: uses HTML5 WebSockets;
connection offloading; supported AMQP clients in Flex +
Silverlight; great at overcoming last-mile hurdles
(firewalls, proxies)</li>
<li>Google Protocol Buffers</li>
</ul></li>
</ul>

<p>Example #1: more hardware!</p>

<ul>
<li>kids invading store works okay for a while, but we hit
contention in the bubble gum machine (DB)</li>
<li>...can scale that DB up really tall, but that's really
expensive?
<ul>
<li>paying per core is paying for peaks... acceptable?</li>
</ul></li>
<li>You cannot buy a product to solve your problems.</li>
</ul>

<p>Example #2: near cache</p>

<ul>
<li>Terracotta: Network attached memory
<ul>
<li>Extend  the JVM threading model across JVMs</li>
<li>In-memory speed access to data</li>
<li>Fully coherent, with stored-to-disk guarantees</li>
<li>Writes sent as deltas across nodes</li>
</ul></li>
<li>Update betting engine; sends to Event Repository in Terracotta,
which ensures others get the update
<ul>
<li>Issue with TC: L2 server can be bottleneck; so shard, or
use $$ version</li>
</ul></li>
</ul>

<p>Example #3: Offload reads to separate systems</p>

<ul>
<li>MySQL replication for history</li>
</ul>

<p>Example #4: Affinity + multi-master replication</p>

<ul>
<li>Customer system backed by replicated LDAP (using 389 server);
customer sticky to a single customer system so that lookups and
writes go to the same system, which means we avoid replication
conflicts because all writes for a single user go to the same
machine</li>
</ul>

<p>Example #5: Scale writes</p>

<ul>
<li>Need to get settlements done quickly -- so they can drop more bets!</li>
<li>More than 10,000 writes/sec</li>
<li>Scale out by using multiple MySQL instances</li>
</ul>

<p>(nice image of how all these fit together; interesting that the
move toward heterogeneous servers was )</p>

<p>Recipes used:</p>

<ul>
<li>Optimize your web front end!</li>
<li>Get rid of static object traffic</li>
<li>Move web data closer to customers</li>
<li><p>Last-mile fan-out messaging</p></li>
<li><p>Data close to buiness logic</p></li>
<li>Read only farms</li>
<li>Multimaster replication</li>
<li>Sharding</li>
</ul>



