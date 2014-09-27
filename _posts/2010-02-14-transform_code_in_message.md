---
tags: javascript messaging design rest
layout: post
title: "Put your transformation code in message?"
---

I've been thinking about architecture recently. One of the
prevailing paradigms is messaging, since it can minimize
coupling, enable scalability, and provides very flexible plumbing
for future extensions.

One of the core problems you need to confront is the payload:
what's in the message? Is it action-based data -- like commands
in <a href="http://www.udidahan.com/2009/12/09/clarified-cqrs/">CQRS</a>?
Data transfer objects? Domain objects?

One scaling strategy is to distribute your load across
machines, which also enables you to update these proceses
independently. Once you get into that realm you have to worry
about versioning the data. You can try and fool yourself into
thinking you'll get the canonical version of the data correct the
first time, but you won't. The world changes too often for this
to happen. Some popular serialization frameworks (protobuf, Avro,
etc.)  make both forward and backward compatibility a priority
for this and other reasons, but they may forbid certain types of
changes (renamings, merging, removing). 

I recently had a random thought about this versioning and
compatibility problem: what if you put references to the code
necessary to transform between versions in the message itself? It
echoes the REST thesis discussion of <a
href="http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_1_7">code-on-demand</a>
-- if your clients are incapable of consuming the media types
you're serving them, give them the tools to do so at runtime.

The idea is that you can build your client to consume a
particular version of a message, and when you get a message of a
different version you ask the message for the code necessary to
transform itself to the version you expect. That code could be
anything -- typically XSLT is used but that presumes the message
is XML. It could also be JavaScript -- the ubiquity of JavaScript
interpreters would make it easy to embed into any sort of
client. And since you wouldn't be sending the code itself, only a
reference (URL whose content can be cached) it's not adding a
huge amount of overhead.

For example:

    Message:
    { 
       version   : '1.2',
       type      : 'Address',
       address1  : '555 Main Street',
       city      : 'Pittsburgh',
       region    : 'PA',
       postal    : '15260',
       country   : 'USA',
       transform : {
           '1.1' : 'http://.../address/1.1_to_1.2.js',
           '1.0' : 'http://.../address/1.0_to_1.2.js'
       }
    }


1. Client receives message, recognizes it as version 1.2.
But it expects version 1.1.
2. Client looks up the transformation script for version 1.1
from the message.
3. Client fetches 'http://.../address/1.1_to_1.2.js' and
executes it with the message as an argument. (Since we're using
HTTP the server can set its cache headers so that the client
doesn't need to do this for every single message.) 
4. From the transformation the client gets its expected
version of the message and continues processing.

You could even add another layer for efficiency by specifying
a resource you can query to get specific resources:

    { 
       version   : '1.2',
       type      : 'Address',
       address1  : '555 Main Street',
       city      : 'Pittsburgh',
       region    : 'PA',
       postal    : '15260',
       country   : 'USA',
       transform : 'http://.../address/transforms.js'
    }
    
    Client: 
      GET http://.../address/transforms.js
    
    Server:
      {
           '1.1' : 'http://.../address/1.1_to_1.2.js',
           '1.0' : 'http://.../address/1.0_to_1.2.js'
      }
    
    ... proceed as before ...

Another variant is to specify a generic resource and execute
it with both the message and the desired version.

Yet another is to return function references as the object
values instead of URLs.

Yet another is to not inlude any transformation reference in
the message at all, relying on the client's knowledge of the
server to be able to look it up as needed. While I like
standalone messages this isn't as crazy as it sounds, and could
rely on work being done in creating an HTTP client workspace so
we can really do HATEOAS. (<a href="http://www.jroller.com/Solomon/">Solomon</a>, among others,
has been banging the drum on this a while, and has some blog
posts about it).

Of course, this is all part of a trade-off -- you're making it
easier to change your messages and for heterogeneous clients to
interact with your system, while imposing some costs on them
(JavaScript interpreter, more complex client that resolves
message diffs at runtime) and on the server (need to distribute a
new 'message migration' every time you change a message).

That said, clearly there are issues with this:

<ul>

  <li>Security risk: you're executing random code off the
  Internet!
  <br />
  <br />
  True, but browsers do this all the time and my impression is
  that we have pretty good sandboxing mechanisms for
  JavaScript. But it could certainly be a showstopper for
  organizations that have a strict policy about this, though it's
  possible that it may be more appropriate for internal/partner
  use than the internet-at-large.</li>

  <li>Won't scale!
  <br />
  <br />
  Maybe. While we're introducing a number of places for clients
  to make things faster (cache the transformation script content,
  cache the compiled transformation script) this could introduce
  too much latency for message systems requiring extremly high
  throughput. However, such systems may typically trade-off
  performance for deployment inflexibility (ensuring all clients
  using same versions), negating the whole need for it.</li>

  <li>You're bloating my messages!
  <br />
  <br />
  True. Though I mentioned one way that would add no data to the
  message at all, the most common way would. It's a trade-off.</li>

  <li>JavaScript sucks!
  <br />
  <br />
  I'm sorry you feel that way. Plugin your favorite dynamic
  language, or even use remotely loaded Java classes
  instead. (.NET probably has something similar.)</li>

</ul>

Anyway, I've probably spent too much time over such an idle
thought.



