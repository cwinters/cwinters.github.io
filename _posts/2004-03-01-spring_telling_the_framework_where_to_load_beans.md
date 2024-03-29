---
tags: config java spring
layout: post
title: "Spring: Telling the framework where to load beans"
---



<p><a href="/2004/02/11/spring_referencing_multiple_bean_config_files.html">Earlier</a> I discussed how to refer to multiple bean definition files in the <tt>DispatcherServlet</tt> declaration in your <tt>web.xml</tt>. But you can also refer to beans not in your WAR file using the <tt>classpath:</tt> prefix:</p>
<pre class="sourceCode">
&lt;servlet>
    ...
    &lt;init-param>
        &lt;param-name>contextConfigLocation&lt;/param-name>
        &lt;param-value>
            <font color="#ff0000">classpath:com/optiron/cd/dao/spring-dao-objects.xml</font>,...
        &lt;/param-value>
    &lt;/init-param>
&lt;/servlet>
</pre>
<p>I don't think this is in the docs, or if it is I missed it. (RC2 is to be released today according to Juergen.) I found it out by opening up the <tt>org.springframework.web.context.support.XmlWebApplicationContext</tt> class and browsing to the <tt>loadBeanDefinitions()</tt> method. There you see a call:</p>
<pre class="sourceCode">
    reader.loadBeanDefinitions(getResource(this.configLocations[i]))
</pre>
<p>Ctrl-B that 'getResource()' call and you'll jump to <tt>org.springframework.context.support.AbstractApplicationContext</tt> where you can easily (it's eight lines of code) dope out how they identify items on the classpath. This process took far longer to type out here than to actually do thanks to IDEA.</p>

<p>What prompted this? I split out the DAO/domain objects into their own entity -- IDEA: "module"; Maven: "project" -- and I didn't want to have to copy the generated <tt>spring-dao-objects.xml</tt> file over to the webapp. Once again, Spring lets you do the right thing...</p>


