---
tags: qcon conference agile operations deployment design modeling
layout: post
title: "QCon 2009: Agile Development to Agile Operations"
---



<p><strong>Stu Charlton, Elastra</strong></p>

<p>(Elastra does automated provisioning and scaling of J2EE apps)</p>

<p>To discuss:</p>

<ul>
<li>How is cloud computing changing the relationship between
development and operations?</li>
<li>Design goals to bridge worlds</li>
<li>Integrating application design, development, and operations</li>
</ul>

<p>Tension between development and ops -> we've done a lot of work
to streamline the development process, but barriers to
operations; different mindsets</p>

<p>Moving to organizationally and geographically distributed design
and operations.</p>

<p>Scalaing and performance complex combination of design and
operations decisions.</p>

<p>Applications and infrastructure management complex and
inter-disciplinary: "What used to be [spec] documents are now
APIs." This is a good and bad thing.</p>

<p>References cloud semi-jokingly as "Scalability without skill;
availability without avarice"</p>

<p>Vendors have stacks of solutions, but there's big culture and
tool gaps due to delivery orientation vs operations
orientation. For instance, IBM has set of tools for devs and set
for ops monitoring, but they're not integrated or provide a
similar view.</p>

<p>How to apply agile practices to operations?</p>

<ul>
<li>Some are useful
<ul>
<li>value thru functionality</li>
<li>automated build, test, integration</li>
<li>autonomous teams</li>
</ul></li>
<li>But not others
<ul>
<li>greater value placed and continuity and risk</li>
<li>test environment: ops is "more like rehearsal"</li>
<li>legacy dependencies</li>
<li>where's the source? that is, "the thing that defines
reality"</li>
</ul></li>
</ul>

<p>Example: why can't servers communicate? Could be:</p>

<ul>
<li>credential management (at many different levels: OS, DB, app)</li>
<li>configuration (same as above)</li>
<li>network config</li>
<li>firewall config</li>
</ul>

<p>Point: your app sits in a context. You don't test that.</p>

<p>Example: what do I need to do to scale out cluster?</p>

<ul>
<li>Other systems:
<ul>
<li>security may need registered</li>
<li>load balancers may need new machines configured to it</li>
<li>monitoring (auto-register available.. but not everywhere)</li>
<li>service desk so you can trace changes</li>
</ul></li>
<li>Architectural issues:
<ul>
<li>stateful or stateless nodes</li>
<li>repartitioning of data</li>
<li>limits/constraints to scale out? (e.g., will it actually
work after adding another node?)</li>
</ul></li>
</ul>

<p>Example: what is authoritative reality?</p>

<ul>
<li>the state something should be in might not be as it should
<ul>
<li>config file changed at runtime; maybe part of your upgrade
changes silently fail; maybe you're affecting other things
in the system you're not even aware of</li>
<li>what are transitioning states for all these systems?</li>
</ul></li>
</ul>

<p>To consider:</p>

<ul>
<li>Configuration as data AND code</li>
<li>Collaboration on design and operations</li>
<li>Account for full value stream of system</li>
</ul>

<p>Design goals:</p>

<ul>
<li>separate applications from infrastructure; how far can we
really go with blackbox platform-as-a-service? there are
dependencies between systems as well</li>
<li>enabling computer to help me with design and operations:
machine learning; IT complexity is getting overwhelming; is
this essential or accidental complexity? can we declare
information in a machine-consumable form and have them learn?</li>
<li>explicit collaboration: little tool support for ops</li>
</ul>

<p>(great image of "approach to integrated design and ops")</p>

<p>Main focus on APIs to-date, mechanisms (via "management plane")</p>

<p>Instead of making it a black box, expose all settings and info;
future focus will be on "control plane"</p>

<p>Many companies looking to do some variation on this in next few
years (Oracle, IBM, VMWare)</p>

<p>Config code, config, models -- what is "source"?</p>

<p>Bottom up view:</p>

<ul>
<li>scripts and recipes: no visibility</li>
<li>run books (coded into workflow engines)</li>
<li>frameworks (e.g., chef, puppet)</li>
<li>build systems (Maven)</li>
</ul>

<p>Top down:</p>

<ul>
<li>Modeled viewpoints (MS Oslo is "turtles all the way down", UML)
e.g., 'network viewpoint', 'storage viewpoint'</li>
<li>Modular containers (OSGI, Spring, Azure roles)</li>
<li>Confg models (SML [Service Modeling Language], CIM; ECML, EDML
-- latter two E is Elastra)</li>
</ul>

<p>Compare to SQL declarativeness</p>

<p>(image: Model Driven Collaboration Design)</p>

<p>OTOH: "All modeling is programming, and all programming is
debugging" - Neil Gunther.</p>

<p>Need visibility into what model implies</p>

<ul>
<li>code generation?</li>
<li>plan generation? (like SQL query planning)</li>
</ul>

<p>Accounting barriers preventing some of this: cost attribution
(capex vs opex for cloud provisioned computing resources); fixed
vs variable cost</p>

<p>vs.</p>

<p>Look at end-to-end system as value stream; costing based on time
calculations for repeatable activities (Time Driven Activity
Based Costing; older idea, but transforming to Lean)</p>

<p>Stu says:</p>

<ul>
<li>Distributed, autonomous control
<ul>
<li>ownership and stewardship of artifacts and systems</li>
</ul></li>
<li>Open document exchange describing system
<ul>
<li>"model marts", CMDB, PIM</li>
<li>contrast with web success at exchanging docs</li>
</ul></li>
<li>Hyperlinked web architecture: <strong>no monolithic docs</strong>
<ul>
<li>we have a lot of experience working with links now</li>
</ul></li>
<li>Model-driven: stradles bridge between code and document</li>
<li>Goal and policy driven: collaborative (leverage social
networks); governable (access control)</li>
</ul>

<p>ECML, EMML, EDML = examples of how to model; apache-licensed</p>

<p>Q+A snippets:</p>

<ul>
<li>Doesn't affect continuous deployment much; they're orthogonal;
models aren't necessarily the monolithic things that people can
think of (greybeards in basement issuing forth "The Model"</li>
<li>Status of tools to create inferences from declarations is poor.</li>
<li>distributed configuration database @ runtime has done a lot in
telecom, not much penetration yet</li>
<li>Federated identity technologies (WS-Federation + SAML); but
directories still the main way to do things; OpenID one way
also, but prone to phishing; can use SAML to login to google,
salesforce right now but it's a PITA</li>
<li>colocated dev/ops to eliminate handoff? some benefit, but
there's still a "shared services" team; it also doesn't solve
the problem <strong>across</strong> teams, nor interdependencies; and worse,
some industries are legally forbidden from doing this (Banking)</li>
</ul>




