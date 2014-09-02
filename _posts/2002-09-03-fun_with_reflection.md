---
tags: java
layout: post
title: "Fun with reflection"
---



In the course of creating the XML files for use in our proposed testing framework (<a href="/2002/09/03/testing_environment_setup.html">overview here</a>), I created a simple file to do it for a bean at a time. It would be nice to be able to run this for multiple beans at a time. Hmm...

<p>(To acclimate: every entity has an associated <tt>Wrapper</tt> session bean which contains all the relationships and queries. Every <tt>Wrapper</tt> has a method <tt>fetchByEntity( String )</tt> method which retrieves all beans in the database with a particular entity number, which is a way of partitioning the data. <tt>EJBClient</tt> is just a service locator with some shortcuts, home caching, etc.)
<pre>
 EJBClient client = new EJBClient();
 DataSerializer ds = new DataSerializer( null );
 String interfaceName = "com.optiron.readi.interfaces.";
 for ( int i = 1; i < argv.length; i++ ) {
     String beanName = argv[i];
     File xmlOutfile = new File( dataDir, beanName + ".xml" );
     ds.setFileSource( xmlOutfile );
     String beanInterface = interfaceName + beanName;
     Class wrapperHomeClass = Class.forName( beanInterface + "WrapperHome" );
     Object wrapperHome = client.getWrapperHome( beanName );
     Method createMethod = wrapperHomeClass.getMethod( "create", null );
     Object wrapper = createMethod.invoke( wrapperHome, null );
     Class wrapperClass = Class.forName( beanInterface + "Wrapper" );
     Method entityMethod = wrapperClass.getMethod(
                              "fetchByEntity", new Class[] { String.class } );
     List items = (List)entityMethod.invoke(
                              wrapper, new String[] { entno } );
     ds.writeXml( items );
     System.out.println( "Wrote bean [" + beanName + "] to " +
                         "[" + xmlOutfile.getAbsolutePath() + "]" );
 }
</pre>

<p>As a result of this and other work done over the weekend, I'm getting more comfortable with
reflection. This is probably a dangerous thing since I use it all the time in Perl :-)


