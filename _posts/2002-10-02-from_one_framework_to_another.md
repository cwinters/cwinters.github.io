---
layout: post
title: "From one framework to another"
---



So the persistence framework (using <a href="http://hibernate.sourceforge.net/">Hibernate</a>) seems to be working swimmingly. I had some fun trying to get the persistent classes to deploy as an MBean -- dependencies, etc. -- but it worked out ok and I learned a little (just a little) about JMX and writing MBeans.

<p>Now it's back to the <a href="/2002/09/19/java_webapp_frameworks.html">earlier referenced decision</a> on web frameworks. After talking it over we've decided to move forward with Struts. A big reason for this was support -- not in the traditional sense, but because Struts is so widespread we'll have an easier time finding books, articles, pattern implementations, etc. Not to mention it will make hiring easier -- this wouldn't be such a big deal if we were a big company, or we had Java gurus on staff, but we aren't and we don't. Additionally, this will be more palatable to clients who expect to be able to extend things themselves.</p>

<p>Time for a crash course on JSP and taglibs...</p>


