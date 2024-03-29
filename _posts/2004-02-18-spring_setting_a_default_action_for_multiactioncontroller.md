---
tags: java spring
layout: post
title: "Spring: Setting a default action for MultiActionController"
---



The Spring web application framework has the notion of a controller, generally mapping to the 'C' in 'MVC'. (See <a href="http://lists.ourshack.com/pipermail/templates/2002-November/003974.html">here</a> for reasons why MVC in GUIs and MVC in webapps may not mean the same thing.) A common controller is one that combines multiple tasks into one class -- searching records, displaying and possibly editing a particular record is a typical usage. Spring implements this with a <a href="http://www.springframework.org/docs/api/org/springframework/web/servlet/mvc/multiaction/MultiActionController.html">MultiActionController</a> (or MAC for this post).

<p>In typical Spring fashion the MAC figures out which action to execute using a <a href="http://www.springframework.org/docs/api/org/springframework/web/servlet/mvc/multiaction/MethodNameResolver.html">MethodNameResolver</a>. A typical implementation (such as <a href="http://www.springframework.org/docs/api/org/springframework/web/servlet/mvc/multiaction/ParameterMethodNameResolver.html">ParameterMethodNameResolver</a>) is to use the value of a GET/POST parameter (e.g., 'action') as the task you wish to run. You tell the resolver which parameter to use in the configuration, which like everything else in Spring is done using the 'bean' tag:</p>
<pre class="sourceCode">
&lt;bean id="<b><font color="#ff0000">actionResolver</font></b>"
    class="org.springframework.web.servlet.mvc.multiaction.ParameterMethodNameResolver">
    &lt;property name="paramName">&lt;value>action&lt;/value>&lt;/property>
&lt;/bean>
</pre>
<p>You then wire together this resolver with your controller, referencing the 'id' attribute of the bean you've configured in the 'ref' tag:</p>
<pre class="sourceCode">
&lt;bean id="myController"
      class="com.optiron.web.MyController">
    &lt;property name="methodNameResolver">
        &lt;ref bean="<b><font color="#ff0000">actionResolver</font></b>"/>
    &lt;/property>
&lt;/bean>
</pre>
<p>And finally map a URL to that controller:</p>
<pre class="sourceCode">
&lt;bean id="urlMapping"
      class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
    &lt;property name="mappings">
        &lt;props>
            &lt;prop key="/user.do">myController&lt;/prop>
        &lt;/props>
    &lt;/property>
&lt;/bean>
</pre>
<p>So a URL: <tt>http://foo/user.do?action=showSearchForm</tt> would execute the method <tt>showSearchForm()</tt> in the class 'com.optiron.web.MyController' which is mapped to the URL <tt>user.do</tt>. Easy enough.</p>

<p>But what happens when the user doesn't specify a value for <tt>action</tt>? This is fairly common -- you just want to use 'http://foo/user.do' instead of appending the query string. The implementation referenced above will throw a <a href="http://www.springframework.org/docs/api/org/springframework/web/servlet/mvc/multiaction/NoSuchRequestHandlingMethodException.html">NoSuchRequestHandlingMethodException</a> with the message "No handling method can be found for request". Oops.</p>

<p>Fortunately, like everything else in Spring you can just implement your own <tt>MethodNameResolver</tt>. All you have to do is implement the <tt>getHandlerMethodName()</tt> method specified by the <tt>MethodNameResolver</tt> interface. Here we'll allow the configuration to specify a parameter name and a default method (I left the imports out for brevity):</p> 
<pre class="sourceCode">
public class DefaultParameterMethodNameResolver
        implements MethodNameResolver
{
    private String paramName, defaultMethod;
   
    public String getHandlerMethodName( HttpServletRequest request )
            throws NoSuchRequestHandlingMethodException

<p>    {
        String name = request.getParameter( paramName );
        if ( StringUtils.isEmpty( name ) )
        {
            name = defaultMethod;
        }
        if ( name == null )
        {
            throw new NoSuchRequestHandlingMethodException( request );
        }
        return name;
    }
   
    public void setParamName( String paramName )
    {
        this.paramName = paramName;
    }
   
    public void setDefaultMethod( String defaultMethod )
    {
        this.defaultMethod = defaultMethod;
    }
}
</pre>
<p>Easy enough. And here's how to configure it, this one with a default task of 'list':</p>
<pre class="sourceCode">
&lt;bean id="<b><font color="#ff0000">actionResolverListDefault</font></b>"
    class="com.optiron.cd.web.DefaultParameterMethodNameResolver">
    &lt;property name="paramName">&lt;value>action&lt;/value>&lt;/property>
    &lt;property name="defaultMethod">&lt;value>list&lt;/value>&lt;/property>
&lt;/bean>
</pre>
<p>Now just reference this bean's ID in your controller, replacing the old one, and you're good to go:</p>
<pre class="sourceCode">
&lt;bean id="myController"
      class="com.optiron.web.MyController">
    &lt;property name="methodNameResolver">
        &lt;ref bean="<b><font color="#ff0000">actionResolverListDefault</font></b>"/>
    &lt;/property>
&lt;/bean>
</pre>
<p>I may wind up implementing something like this in OpenInteract2. In fact, as much as OI2 is already a Spring-like framework (with only bits of AOP here and there) it would be interesting to see if it could be configured in much the same way...</p>


