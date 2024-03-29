---
tags: qcon conference soa scalability performance serialization
layout: post
title: "QCon 2009: SOA at eBay"
---



<p><strong>Sastry Malladi, eBay</strong></p>

<ul>
<li>Distinguished Engineer; building large systems for ~20 years</li>
</ul>

<p>SOA is journey</p>

<p>History: </p>

<ul>
<li>one of the first to expose APIs/services</li>
<li>support REST as well as SOAP (former supported way more)</li>
<li>lots of feedback, lots of evolution</li>
<li>early adopters of SOA governance automation</li>
<li>continuously improving architecture with 3 goals: agility,
innovation and operational excellence</li>
</ul>

<p>Stack:</p>

<ul>
<li>mix of optimized, custom SOA framework as well as BoB + open
source components</li>
</ul>

<p>Goals:</p>

<ul>
<li>organize enterprise as set of business functions</li>
<li>reduce cost of developing new features (and reduce cost of
failure)</li>
<li>encourage + enable new business opportunities</li>
</ul>

<p>Practical standpoint, what is SOA?</p>

<ul>
<li>architecture to move from brittled, hardwired application silos</li>
<li>to shared, reusable services</li>
<li>that eliminates redudnacy and enables agility</li>
</ul>

<p>SOA: not just technology (tech + process + people)</p>

<p>Common misconceptions:</p>

<ul>
<li>SOA is new, just a paradigm applied to existing tech</li>
<li>implies WS + SOAP: actually not, REST with JSON/K-V pairs is
equally popular, if not more</li>
<li>end to itself: no, just a means to enable agility</li>
<li>services dev from ground up: always leverage existing
functionality, but morph into services</li>
<li>at dev time, consumers + use cases are known: can evolve</li>
</ul>

<p>Challenges in largescale deployments</p>

<p>Technical:</p>

<ul>
<li>Additional latencies due to multihop</li>
<li>Debugging/tracing is harder</li>
<li>Need efficient request/session caching (contextual cache; you
don't want to jam it in the message; or make it part of the contract)</li>
<li>Security/monitoring challenges</li>
<li>Lots of standards, pick one!</li>
</ul>

<p>Operational</p>

<ul>
<li>Dev adoption + learning curve</li>
<li>Governance</li>
<li>Migrating existing apps</li>
<li>Updates to existing tools + processes</li>
<li>Deployment + rollout</li>
<li>Measuring ROI</li>
</ul>

<p>Further:</p>

<ul>
<li>Co-existence of old and new tech during transition</li>
<li>Supporting internal and external clients that have different
protocols/data binding needs for the <strong>same deployment</strong></li>
<li>QoS and SLA management: very low latency needs, huge traffic</li>
<li>Integration testing: can do functional testing of your own
service, so how do you test in absence of dependencies? service
virtualization, where you can express your dependencies and
it's autosetup for you in test env</li>
<li>High availability and scalability: high volume, low latency</li>
<li>Decompose existing app and migrate legacy services</li>
</ul>

<p>Operational:</p>

<ul>
<li>Version and dependecy management: esp related to high change velocity</li>
<li>Impact to existing tools/env</li>
<li>Time to market pressure: pressure will ALWAYS be there, must
factor in design process</li>
<li>Strong but simple governance, esp w lots of services and high
velocity of changes; point is not just bureaucracy, but to help
you achieve consistency across org</li>
</ul>

<p>How is eBay addressing</p>

<p>Technical:</p>

<ul>
<li>Light and fast platform (homegrown + commercial + open source
components)</li>
<li>Unified testing f/w and service virtualization (ITKO)</li>
<li>Model driven service decomposition; did this methodically and
it yes, it took time, but it paid off</li>
<li>Support for REST + SOAP from start; how is the interface
declared for the REST service? WSDL 2.0 has the notion of
bindings, including an HTTP binding; ebay uses WSDL 1.1, but
includes a concrete way of binding to the REST service</li>
</ul>

<p>Operational:</p>

<ul>
<li>One of the first to automate governance and lifecycle
management</li>
<li>Incremental service deployment: can deploy different services
separately based on dependencies declared (?)</li>
<li>Strong operational management tools</li>
<li>Developer training and incentives for being good citizen;
includes training for designing good services</li>
<li>Formal process to measure adoption + process; haven't
formalized ROI measurement</li>
</ul>

<p>How many services at eBay?</p>

<ul>
<li>internal: several hundred</li>
<li>external: ??</li>
</ul>

<p>eBay SOA Platform:</p>

<ul>
<li>framework: overhead &lt; 5 ms</li>
<li>monitoring: customizable, for internal people only; using SNMP;
service registers events, and aggregators (within the JVM);
these get put into OLAP cubes; eventually they get into a dashboard</li>
<li>security: XACML/WS-Policy based extensible authen/authz</li>
<li>rate limiting: enforcing capacity, budgeting, traffic control;
use XACML to express these</li>
<li>service registry and repository: governmance, lifecycle mgt;
bought SOA software Repository Manager</li>
<li>ESB: for routing, transformations, and mediations (use
opensource for this, Apache Synapse)</li>
<li>orchestration engine: <strong>Q</strong> how different than ESB? <strong>A</strong> ESB
for matching requester and responder for protocol, message
type, whether to use sync/async, etc. Several ESBs mingle in
the rules for orchestrating. But generally, orchestration is
more of a process (BPEL) -- example of getting watched items,
which fetches the watched items, the latest prices for each,
transforms the data into only what's necessary, then returns.</li>
<li>dev tools (eclipse plugin) for service/consumer development;
very concerned with making things simple, otherwise things
won't go anywhere; never leave the IDE space, even for testing</li>
<li>ops tools (management, monitoring, alerting)</li>
</ul>

<p><strong>Q:</strong> Your end user experience is synchronous, but your services
and coordination are async? Is that a tension? <strong>A:</strong>
Absolutely. It took several years to get that absolutely
right. Not all services are equal, which impacts the routing
rules. Sometimes the traffic goes point-to-point and is
synchronous.</p>

<p>Highlights of framework:</p>

<ul>
<li>Declarative pipeline high performance architecture</li>
<li>Request and response decoupling</li>
<li>Protocol and data binding agnostic service
<ul>
<li>same service instance can be invoked using multiple
protocols and formats -- NOT like JBI which requires
normalization; natively serialize and deserialize (more
later -- protocol plugins do this)</li>
<li>no message normalization or conversations</li>
</ul></li>
<li>Pluggable data formats
<ul>
<li>OOB support for SOAP, JSON, Binary XML</li>
<li>Streaming support + attachment support</li>
<li>WSDL </li>
</ul></li>
<li>Pluggable transports, including local </li>
</ul>

<p>Use JAXB for pluggable data formats; use streaming XML api +
stream readers/writers custom written for JSON, key value pairs,
etc. No intermediate format, avoids extra conversion. (Lots of
work done on this that I missed a bit)</p>

<p>Stuff about SOA Governance: my takeaway is that it's declarative;
heard this a lot in the last few days. Enables consistent review,
change management, dependency management. Automated tools using
XQuery to ensure that WSDL matches what's expected.  Also,
reconciling what you find at runtime vs what you expect to find
from your design.</p>

<p>Summary:</p>

<ul>
<li>Solving tech part is relatively easy. Easier than solving
operational aspects -- must do from beginning.</li>
<li>Up front design and modeling of contract/interface, including
granularity is very important.</li>
<li>Service layering, dependency + version mgt must be well thought
through. </li>
<li>Invest up front in governance, testing tools, developer
training.</li>
</ul>



