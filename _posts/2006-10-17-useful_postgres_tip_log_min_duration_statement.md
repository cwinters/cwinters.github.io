---
tags: database postgres
layout: post
title: "Useful Postgres tip: log_min_duration_statement"
---



<p>In your $PG_HOME/postgresql.conf:</p>

<pre>
log_min_duration_statement (integer)

<p>    Logs the statement and its duration on a
single log line if its duration is greater than 
or equal to the specified number of milliseconds. 
Setting this to zero will print all statements 
and their durations. Minus-one (the default) 
disables the feature. For example, if you set it 
to 250 then all SQL statements that run 250ms or 
longer will be logged. <b>Enabling this option can 
be useful in tracking down unoptimized queries in 
your applications.</b>
</pre>


