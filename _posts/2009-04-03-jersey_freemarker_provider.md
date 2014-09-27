---
tags: rest jersey java
layout: post
title: "A Jersey Freemarker Provider"
---

<b>UPDATE:</b> This is now 
<a href="http://github.com/cwinters/jersey-freemarker/tree/master">on github</a>.

There's no built-in Freemarker support in Jersey, which is
fine: no reason to support every view technology under the
sun. Particularly when Jersey makes it so easy to
integrate. There's only one implementation I found, 
<a href="http://markmail.org/message/rz4wjmips66ejues">this item</a>
on the jersey mailing list.[1] For reference, there's also 
<a href="http://blogs.sun.com/sandoz/entry/mvcj">a blog entry from
Mr. Jersey</a> about how to use JSP and "implicit views", but it
references Freemarker rather than providing an example. (I'm not
a fan of implicit views because I like to have the flexibility of
sending other objects than my resource to the template.)

Anyway, my example is similar to the one I found but uses the
servlet context to load the templates vs the classpath, and also
allows you to configure where those templates are stored in your
webapp. It's also got support for loading a
<tt>freemarker.properties</tt> from the classpath and passing a
<tt>Map</tt> to your view instead of a resource.

So here's another starting point for someone, with a few
caveats:

* It works for me, in my little application.
* It just dumps errors out to the web page (easy fix: don't
  break stuff, duh).

{% highlight java %}
package com.cwinters.jersey;

import com.sun.jersey.spi.template.TemplateProcessor;
import freemarker.cache.WebappTemplateLoader;
import freemarker.template.Configuration;
import freemarker.template.Template;
import org.apache.log4j.Logger;
import javax.servlet.ServletContext;
import javax.ws.rs.core.Context;
import javax.ws.rs.ext.Provider;
import java.io.*;
import java.net.MalformedURLException;
import java.util.*;

/**
 * Match a Viewable-named view with a Freemarker template.
 *
 * <p>You can configure the location of your templates with the
 * context param 'freemarker.template.path'. If not assigned
 * we'll use a default of <tt>WEB-INF/templates</tt>. Note that this uses
 * Freemarker's {@link freemarker.cache.WebappTemplateLoader} to
 * load/cache the templates, so check its docs (or crank up the logging
 * under the 'freemarker.cache' package) if your templates
 * aren't getting loaded.</p>
 *
 * <p>This will put your Viewable's model object in the template
 * variable "it", unless the model is a Map. If so, the values
 * will be assigned to the template assuming the map is of
 * type <tt>Map<String,Object></tt>.</p>
 *
 * Example of configuring the template path:
 *
 * <pre>
 * <web-app ...
 *    <display-name>Awesomeo 2000</display-name>
 *    <context-param>
 *       <param-name>freemarker.template.path</param-name>
 *       <param-value>/WEB-INF/views</param-value>
 *   </context-param>
 *   ...
 *</pre>
 *
 * <p>You'll also need to tell Jersey the package where this provider
 * is stored. Typically this is through the servlet's init params -- for instance,
 * in the below configuration we could store this in <tt>com.myco.jersey</tt> and
 * my resources in <tt>com.myco.jersey.resource</tt></p>
 *
 * <pre>
 * <servlet>
 *     <servlet-name>My REST App</servlet-name>
 *     <servlet-class>com.sun.jersey.spi.container.servlet.ServletContainer</servlet-class>
 *     <init-param>
 *         <param-name>com.sun.jersey.config.property.packages</param-name>
 *         <param-value>com.myco.jersey;com.myco.jersey.resource</param-value>
 *     </init-param>
 * </servlet>
 * </pre>
 *
 * @author Chris Winters <chris@cwinters.com>
 */
@Provider
public class FreemarkerTemplateProvider implements TemplateProcessor
{
    private static final Logger log = Logger.getLogger( FreemarkerTemplateProvider.class );

    private static Configuration fmConfig;

    private ServletContext servletContext;
    private String rootPath;

    public FreemarkerTemplateProvider() {}

    public String resolve( final String path )
    {
        if ( log.isDebugEnabled() )
            log.debug( "Resolving freemarker template path (" + path + ")" );

        // accept both '/path/to/template' and '/path/to/template.ftl'
        final String filePath = path.endsWith( "ftl" ) ? path : path + ".ftl";
        try {
            final String fullPath = rootPath + filePath;
            final boolean templateFound = servletContext.getResource( fullPath ) != null;
            if ( ! templateFound )
                log.warn( "Template not found [Given path: " + path + "] " +
                          "[Servlet context path: " + fullPath + "]" );
            return templateFound ? filePath : null;
        }
        catch ( MalformedURLException e ) {
            log.warn( "Caught MalformedURLException when trying to get freemarker resource (" + filePath + ") " +
                      "from the servlet context: " + e.getMessage() );
            return null;
        }
    }

    @SuppressWarnings( { "unchecked" } )
    public void writeTo( String resolvedPath, Object model, OutputStream out ) throws IOException
    {
        if ( log.isDebugEnabled() )
            log.debug( "Evaluating freemarker template (" + resolvedPath + ") with model of type " +
                       ( model == null ? "null" : model.getClass().getSimpleName() ) );

        out.flush(); // send status + headers

        final Template template = fmConfig.getTemplate( resolvedPath );
        if ( log.isDebugEnabled() )
            log.debug( "OK: Resolved freemarker template" );

        final OutputStreamWriter writer = new OutputStreamWriter( out );

        final Map<String,Object> vars;
        if ( model instanceof Map ) {
            vars = new HashMap<String, Object>( (Map<String, Object>)model );
        }
        else {
            vars = Util.stringKeyMap( "it", model );
        }

        // put other globally accessible template items here, like:
        // vars.put( "spring", myApplicationContext );

        try {
            template.process( vars, writer );
            if ( log.isDebugEnabled() )
                log.debug( "OK: Processed freemarker template" );
        }
        catch ( Throwable t ) {
            log.error( "Error processing freemarker template @ " + resolvedPath + ": " + t.getMessage(), t );
            out.write( "<pre>".getBytes() );
            t.printStackTrace( new PrintStream( out ) );
            out.write( "</pre>".getBytes() );
        }
    }

    @Context
    public void setServletContext( final ServletContext context )
    {
        this.servletContext = context;

        fmConfig = new Configuration();

        rootPath = context.getInitParameter( "freemarker.template.path" );
        if ( Util.isBlank( rootPath ) ) {
            log.info( "No 'freemarker.template.path' context-param, " +
                      "defaulting to '/WEB-INF/templates'" );
            rootPath = "/WEB-INF/templates";
        }
        rootPath = rootPath.replaceAll( "/$", "" );

        fmConfig.setTemplateLoader( new WebappTemplateLoader( context, rootPath ) );

        final InputStream fmProps = context.getResourceAsStream( "freemarker.properties" );
        if ( fmProps != null ) {
            try {
                fmConfig.setSettings( fmProps );
                log.info( "OK: Assigned freemarker configuration from 'freemarker.properties'" );
                return;
            }
            catch ( Throwable t ) {
                log.warn( "Failed to load/assign freemarker.properties, will use default settings " +
                          "instead; error: " + t.getMessage() );
            }
        }

        fmConfig.setNumberFormat( "0" );
        fmConfig.setLocalizedLookup( false );
        fmConfig.setTemplateUpdateDelay(0);

        log.info( "OK: Assigned default freemarker configuration" );
    }
}
{% endhighlight %}

And here's an example of how to use it:

{% highlight java %}
package com.cwinters.jersey;

import com.sun.jersey.api.view.Viewable;
import javax.ws.rs.*;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;

@Path( "/foo" )
public class FooResource
{
    private FooDatastore _fooDatastore;
   
    @GET
    @Produces( MediaType.TEXT_HTML )
    public Viewable getBlank()
    {
        return new Viewable( "/foo/form.ftl", new Foo() );
    }

    @Path( "/{id}" )
    @GET
    @Produces( MediaType.TEXT_HTML )
    public Viewable getItem( @PathParam( "id" ) final long id )
    {
        final Foo foo = _fooDatastore.get( id );
        final Map<String,Object> vars = new HashMap<String,Object>();
        vars.put( "it", foo );
        vars.put( "lookups", _fooDatstore.listLookups() );
        return new Viewable( "/foo/view.ftl", vars );
    }

    public void setFooDatastore( final FooDatastore fd )
    {
        _fooDatastore = fd;
    }
}
{% endhighlight %}

Then, assuming your templates are configured with the default,
lay them out like this:

    + WEB-INF
      + templates
        + foo
          - form.ftl
          - view.ftl

----

[1] Confession: I found this only after writing my own. I'd
actually read this thread before but somehow missed the
attachment to the message.




