---
tags: programming
layout: post
title: "Query objects vs. SQL"
---

Two recent blog entries from 
<a href="http://www.rollerweblogger.org/comments/roller/main/refactoring_roller">David Johnson</a> 
and 
<a href="http://blog.hibernate.org/cgi-bin/blosxom.cgi/2003/12/01#qbc">Gavin King</a> 
discuss object-based querying. This falls under the category of "I don't get
it." No offense to David (honest!), but compare this:

{% highlight java %}
public List getTodaysReferers(WebsiteData website) throws RollerException {
  if ( website==null ) throw new RollerException("Website is null");
  QueryFactory factory = mStrategy.getQueryFactory();
  Query query = factory.createQuery(RefererData.class.getName());                
  Condition specifiedUser = factory.createCondition(
      "website", Query.EQ, website);            
  Condition hasDayHits = factory.createCondition(
      "dayHits", Query.GT, new Integer(0));            
  Condition userEnabled = factory.createCondition(
      "website.user.userEnabled", Query.EQ, new Boolean(true));            
  List conditions = new LinkedList();
  conditions.add(specifiedUser);
  conditions.add(hasDayHits);
  conditions.add(userEnabled);                
  query.setWhere(factory.createCondition(Query.AND, conditions));            
  query.setOrderBy(Query.DESC, "dayHits");       
  return query.execute();
}
{% endhighlight %}

To this:

{% highlight java %}
public Collection getTodaysReferers( String website ) {
  return runQuery(
    "website = ? AND dayHits = 0 AND userEnabled = 1 ORDER BY dayHits DESC",
    new Object[] { website },
    new Class[] { String.class } );
}
{% endhighlight %}

Or to use Gavin's example of:

{% highlight java %}
session.createCriteria(Project.class)
  .createDisjunction()
      .add( eq("name", "Hibernate") )
      .add( like("description", "%ORM%") )
  .list();
{% endhighlight %}

Versus:

{% highlight java %}
return runQuery( "name = ? AND description LIKE ?",
  new Object[] { "Hibernate", "%ORM%" },
  new Class[] { String.class, String.class } );
{% endhighlight %}

(And this is assuming that we even need the classes to define what the
placeholders are, that we're not using something like the SQL library in
Spring, etc.) 

I really feel like I'm missing something here. Gavin and Dave are smart guys
and from what I've seen very practical as well. But why would you use the query
by criteria type of code at all? It's more difficult to read, for one, and has
more code (~~ more errors). The query as string is also much easier to
integrate with an existing library of queries, even with a phrasebook of
queries created by the database folks who are for some reason treated like
peasants by many programmers. 

I do recognize that you can use such a framework to isolate you from changes
in basic SQL -- translating the PostgreSQL pattern matching to other systems
can be a PITA, for example. But is it really worth the added obfuscation? 

So many programmers treat SQL and database folks like some <a
href="http://www.snpp.com/episodes/1F16.html">booger man</a> and I still don't
understand why. Is it because SQL is easy to learn and understand? (I can teach
my wife SQL basics in 15 minutes. Java basics?) Because it's been around for 20
years and is tainted with some legacy virus? (Darn that historical knowledge?)
Because lots of interesting SQL isn't really portable from vendor to vendor?
(You probably switch databases fewer times than you switch programming
languages, and that doesn't stop you from using Java or Perl, does it?) 

I know that database people sometimes can be a PITA. Working without many
modern programming language constructs for a long time can do that to you. But
many of those database people have seen application frameworks arrive with a
huff and fall by the wayside after the CTOs and managers who championed them
left to spread their overengineering ways elsewhere.


