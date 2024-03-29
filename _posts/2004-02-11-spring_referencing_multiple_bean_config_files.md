---
tags: java servlet spring
layout: post
title: "Spring: Referencing multiple bean config files"
---



For our new project we're using Spring inside a webapp instead of deploying an EJB container. For now Spring is doing duty as a IoC container, Hibernate wrapper and minimal webapp framework. We'll probably add some AOP stuff a little later. I'm really happy with it so far and hope they're able to keep a focus on simplicity as the project matures.

<p>So after a little initial work I wrote a new code generation system. It's much smaller than our existing one -- I'm probably not going to automate the relationship and finder methods -- and generates the domain objects, DAO interfaces and Hibernate DAO implementations from the Hibernate mapping files. It also generates the Spring bean declarations in a separate XML file.</p>

<p>However, I already had a bean configuration file: when deployed using the DispatcherServlet Spring looks for a <tt>/WEB-INF/${servlet_name}-servlet.xml</tt> file. This contains the Hibernate session factory declaration, datasource connection information, web application mappings, etc. So how to reference the separate XML file create during code generation? (This is probably in the docs somewhere, but I didn't see it at first glance....)</p>

<p>One of the nice things about Spring is that it operates like you think it should. You think: "Well, I just tell Spring to load multiple configurations." Ok, do a little research and see that it's no problem. Cool. Next: "<b>How</b> do I tell Spring about my configuration files?" Answer: where you initialize Spring, from the servlet configuration in <tt>web.xml</tt>:</p>
<pre class="sourceCode">
&lt;servlet>
    &lt;servlet-name>spring&lt;/servlet-name>
    &lt;servlet-class>org.springframework.web.servlet.DispatcherServlet&lt;/servlet-class>
    &lt;load-on-startup>1&lt;/load-on-startup>
    &lt;init-param>
        &lt;param-name>contextConfigLocation&lt;/param-name>
        &lt;param-value>/WEB-INF/spring-dao-objects.xml,/WEB-INF/spring-servlet.xml&lt;/param-value>
    &lt;/init-param>
&lt;/servlet>
</pre>

<p>Works like a charm!</p>


