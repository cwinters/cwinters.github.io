---
tags: design oi2 perl
layout: post
title: "Using REST params in OI2"
---



<p>A couple days ago <a
href="http://www.cwinters.com/news/display/?news_id=3342">I
discussed</a> the first part of getting REST params into OI2 --
parsing the URL and storing the parameters. Now, what do we do with
them?</p>

<p>It's probably useful to point out that none of what I'm about to
discuss is actually necessary -- it's just a shortcut. But useful (and
hopefully intuitive) shortcuts like these are one of the factors that
make a framework successful. The trick is to find a balance between
external configuration (which can be hard for users to find) and
internal coding (which users are reluctant to change because of
unknown side effects). To find the balance it's usually best to do it the long way first -- sometimes you might find that the long way isn't so long after all.</p>

<p>So, the long way to use the parameters would be like this:</p>
  
<pre class="sourceCode">
sub do_something {
    my ( $self ) = @_;
    my $request = CTX->request;
    my @params = $request->param_url_additional();
    $self->param( foo_id  => $params[0] ) if ( $params[0] );
    $self->param( foo_num => $params[1] ) if ( $params[1] );
    ...
</pre>
  
<p>Given the URL: 'http://foo/do_something/8438/9100' the parameter
'foo_id' would get be assigned '8438' and 'foo_num' '9100'. Pretty
straightforward. But every task has to fend for itself to match up the
positional parameters to what it expects -- the 'do_something' might
expect 'foo_id' and 'foo_num', but the 'list_something' might just
expect 'foo_num'. As a result you'll wind up doing is extracting those
assignments out and creating a method in every action like this:</p>
  
<pre class="sourceCode">
sub _assign_params_from_url {
    my ( $self ) = @_;
    my $request = CTX->request;
    my @params = $request->param_url_additional();
    return unless ( scalar @params );
    if ( 'do_something' eq $self->task ) {
        $self->param( foo_id  => $params[0] ) if ( $params[0] );
        $self->param( foo_num => $params[1] ) if ( $params[1] );        
    }
    elsif ( 'list_something' eq $self->task ) {
        $self->param( foo_num  => $params[0] ) if ( $params[0] );
    ...
 
sub do_something {
    my ( $self ) = @_;
    $self->_assign_params_from_url;
    ...
</pre>
  
<p>This isn't bad, but we can do better. It's a great candidate for
pulling the decision and assignment into configuration. Why?</p>
  
<ul>
  <li>The differentiating factor is known to us beforehand. In this
  case it's the task name. If it's something at runtime -- such as
  choosing which query to run based on whether certain parameters are
  defined -- then it's probably a good idea to do it in code.</li>
  <li>The code you'd use is very repetitive and simple, basically just
  a case statement.</li>
  <li>The concepts map pretty well -- all we're providing a list of
  parameter names to map to a list of parameter values</li>
</ul>
  
<p>The configuration would look like this:
  
<pre class="sourceCode">
# in conf/action.ini for your package
[myaction url_additional]
do_something  = foo_id
do_something  = foo_num
list_someting = foo_num
 
# now in your code:
 
sub do_something {
    my ( $self ) = @_;
    # ... 'foo_id' and 'foo_num' parameters are already set
 
sub list_something {
    my ( $self ) = @_;
    # ... 'foo_num' parameter already set
</pre>
 
<p>So hopefully you'll see this implemented on my site shortly...</p>



