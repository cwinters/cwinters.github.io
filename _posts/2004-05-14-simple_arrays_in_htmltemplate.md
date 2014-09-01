---
layout: post
title: "Simple arrays in HTML::Template"
---



Are you an HTML::Template user? Can you tell me how to display simple scalars (versus hashrefs) in an array? To put it more concretely, I have something like the following in Template Toolkit:
<pre class="sourceCode">
my @names = qw( John Paul Ringo );
my $template = Template->new();
$template->process( \*DATA, { names => \@names } );
__DATA__
You listed the following names:

</pre>
<p>Is there an equivalent in HTML::Template? Because from looking over the docs it appears I need to move the data into hashrefs within the array, which is really annoying if you're trying to build a framework that works on multiple templating systems:</p>
<pre class="sourceCode">
my @names = ( { name => 'John' },
              { name => 'Paul' },
              { name => 'Ringo' } );
my $template = HTML::Template->new( filehandle => *DATA  );
$template->param( names => \@names );
print $template->output();
__DATA__
You listed the following names:
&lt;TMPL_LOOP NAME="names">
  * &lt;TMPL_VAR NAME="name">
&lt;/TMPL_LOOP>
</pre>


