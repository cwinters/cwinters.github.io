---
tags: rest dataexchange
layout: post
title: "Thinking data publishing formats, again"
---



<p>
    Two years ago we were rebuilding 
    <a href="http://healthcare.vocollect.com/">AccuNurse</a> and I had
    this idea we could expose all the data as REST resources. All
    access to the data, including from the webapp via AJAX, would be
    via GET/PUT/POST messages.
</p>

<p>
   That architecture has a lot of benefits, but I didn't have enough
   experience with the architecture to design it properly nor time to
   learn as we went, particularly since we were rethinking an earlier
   version rather than straight-up rewriting it.[1] 
</p>
   
<p>
   So we fell back to a standard (in our company) Java web stack:
   Struts2 (then WebWork), Hibernate, Spring. It's okay, nothing
   special. It has the undervalued benefit of being easy to teach to
   new people and has a fairly straightforward execution path, so it's
   not difficult to debug when things blow up.
</p>

<p>
   I figured the REST ideas would come back when we started
   integrating with other systems, primarily clinical software. In
   nursing homes these would be the systems that do billing, manage
   prescriptions and the medical record.
</p>

<p>
   However, that's not the case. Such integration has been
   well-defined by <a href="http://www.hl7.org/">HL7</a>. And the
   summary data we export for reporting to Medicare/Medicaid already
   has integration paths defined (not as well defined, but good
   enough). Bummer.
</p>

<p>
   But it's now popping up again. We're thinking about exposing much
   of our data for... some unspecified reason. It may be customer pull
   (e.g., "we want our data!") or partner pull (e.g., clinical
   partners interested in getting supporting data from us to fully
   populate electronic medical records).
</p>

<p> 
   Given such loose requirements and the amount of other work we have
   to do, my natural tendency is just to wait and see what
   happens. But I know in my bones that exposing our data in the right
   way can lead to immense utility that we can't even conceive right
   now.[2] And while being able to define <b>how</b> that's done
   is very powerful, being able to define how it's <b>not</b> done
   frees us from a great deal of future pain. (I'm not sure which is
   the greater motivator at this point.)
</p>

<p>
   But unless you've got scads of money and a large development team
   (we have neither), you simply cannot invest a huge amount of time
   and resources getting such a system up and running on these
   somewhat vague but powerful ideas, and secondary ones at that
   (our business model does not include to building a platform).
</p>

<p>
   So getting something useful quickly working is A Big Deal. I don't
   know much about the choices in this area, but here's what I do
   know, with big overlaps among them:
</p> 

<ul>

   <li>Rolling your own. Always an option. Build on top of Restlet or
   JAX-RS, plus some resource-customizable search abilities. Need to
   define or reuse someone else's data format</li>

   <li><a href="http://code.google.com/apis/gdata/">GData</a>: This is 
   a generic data format, lots of tool support,
   plus other platforms 
   <a href="http://wiki.apexdevnet.com/index.php/Google_Resource_Center">like
   Salesforce</a> use it. There is a flavor of GData for health
   information, but it's really for interacting with Google Health
   rather than defining a generic health data interchange format. (At
   least AFAICT.)</li>

   <li>Atomserver: Looks like it sits on top of GData or any other
   format.</li>

   <li>Abdera: Infrastructure behind Atomserver if baremetal needed.</li>   

</ul>

<p>
   For any of these it seems like there's a marshalling/unmarshalling
   layer needed, whether it's using XML, JSON, YAML, whatever. (Is
   this baked into GData?) And IME that's always a gigantic pain no
   matter what language you use. Maybe it's gotten better since the
   last time I looked?
</p>

<p>
   Finally, I'm still a little fuzzy on how publishing large amounts
   of potentially rapidly changing data with Atom works, or at least
   how clients are expected to use it. Maybe I do understand it but
   it's just not that complicated, and all the examples (using blogs)
   just muddy the issue. This begs the question: Is there a niche for
   articles/blogposts about our sort of use?
</p>

<p>
   A few references:
</p>

<ul>
  <li>
    <a href="http://radar.oreilly.com/archives/2006/07/a-week-in-the-valley-gdata.html">A Week in the Valley: GData</a>
  </li>
  <li>
    <a href="http://www.dehora.net/journal/2007/06/app_on_the_web_has_failed_miserably_utterly_and_completely.html">APP on the Web has failed: miserably, utterly, and completely</a>
  </li>
  <li>
    <a href="http://www.25hoursaday.com/weblog/2007/06/09/WhyGDataAPPFailsAsAGeneralPurposeEditingProtocolForTheWeb.aspx">Why GData/APP Fails as a General Purpose Editing Protocol for the Web</a>
  </li>
  <li>
    <a href="http://code.google.com/apis/health/">Google Health Data API</a>
  </li>
</ul>

<hr noshade="noshade" width="50%" />

<p>
   <em>[1]</em> Plus the REST infrastructure wasn't fully baked
   in the Java world -- <a href="http://www.restlet.org/">Restlet</a>
   was still in beta (though during my investigation I contributed 
   some fixes and wrote a little demo app that circulated for a bit), and 
   <a href="http://jersey.dev.java.net/">JAX-RS</a> hadn't kicked off
   yet.
</p>

<p>
   <em>[2]</em> You might insert standard Web 2.0 argument here. But
   these applications are internal to a nursing home or chain, and I'm
   not certain what traction we'd get as a mashup platform in such an
   environment. I think it can happen because there's a lot of useful
   information to be gleaned by the type of data we gather, but I
   don't know how many in the industry have the mindset to do
   so. Maybe if everyone went to 
   <a href="http://www.defragcon.com/">Defrag</a> that might 
   change -- I hope to go next year.
</p>



