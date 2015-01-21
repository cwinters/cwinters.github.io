---
title: "Today I remembered: psql exporting CSV"
layout: post
tags: "postgres commandline database shell"
---

Normally these are titled "Today I Learned", but this set of actions is one I
built up in past jobs but forgot.

If you're using Postgres the `psql` tool is one you should be familiar with.
There are lots of tips posts out there on it (like 
[Craig Kerstiens](http://www.craigkerstiens.com/2013/02/21/more-out-of-psql/) 
and [Selena Deckelmann](https://www.google.com/?q=psql%20site%3Achesnok.com))
but this is one of mine.

## Simple things: use \COPY

There are, of course, a couple ways to do this. If you have a simple query then
`\COPY` is very nice:

    mydb=> \COPY (select * from auth_user where last_name ilike 'w%') to 'w_users.csv';

It allows you to fiddle with delimiters as well:

    mydb=> \COPY (select * from auth_user where last_name ilike 'w%') to 'w_users.csv' with delimiter ',';

and since it's just a query you can do formatting:

    mydb=> \COPY (select id, first_name, to_char(date_joined, 'yyyy-MM-dd') from auth_user where last_name ilike 'w%') to 'w_users.csv' with delimiter ',';

That file can also be brought in with `\COPY` -- here we'll load that set of
users to a table named `user_subset`:

    mydb=> \COPY user_subset from 'w_users.csv';

The nice thing about `\COPY` is that it works on your local filesystem, whereas
the plain `COPY` works only on the server's filesystem. However, `\COPY` only
works in `psql` and `COPY` is supported by some (most?) APIs out there -- see
[node](https://github.com/brianc/node-pg-copy-streams) or
[Go](http://godoc.org/github.com/lib/pq#hdr-Bulk_imports) for examples.

## Everything else: psql and output formatting

All that said, with a more substantial query you get into issues with
formatting and parens and such and `\COPY` doesn't work as well -- for example,
try to break up the above query with formatting onto multiple lines.

This is where the `psql` formatting flexibility comes in. You can ask `psql`
for what you can do with `\?` and you'll see these sets among the options:

    Input/Output
      \copy ...              perform SQL COPY with data stream to the client host
      \echo [STRING]         write string to standard output
      \i FILE                execute commands from file
      \ir FILE               as \i, but relative to location of current script
      \o [FILE]              send all query results to file or |pipe
      \qecho [STRING]        write string to query output stream (see \o)
    ...
    Formatting
      \a                     toggle between unaligned and aligned output mode
      \C [STRING]            set table title, or unset if none
      \f [STRING]            show or set field separator for unaligned query output
      \H                     toggle HTML output mode (currently off)
      \pset NAME [VALUE]     set table output option
                             (NAME := {format|border|expanded|fieldsep|fieldsep_zero|footer|null|
                             numericlocale|recordsep|recordsep_zero|tuples_only|title|tableattr|pager})
      \t [on|off]            show only rows (currently off)
      \T [STRING]            set HTML <table> tag attributes, or unset if none
      \x [on|off|auto]       toggle expanded output (currently off)

Here's how you can use them. First, the difference between aligned and
unaligned mode is obvious when you see it. Here's aligned:

    loadtest=> select id, first_name, last_name, date_joined from auth_user order by id desc limit 10;
       id   | first_name |  last_name  |          date_joined
    --------+------------+-------------+-------------------------------
     109699 | LILLIE     | CHRISTENSEN | 2015-01-07 16:32:27.204538+00
     109698 | VERA       | WOLF        | 2015-01-07 16:32:27.111546+00
     109697 | MARCO      | BENSON      | 2015-01-07 16:32:27.028772+00
     109696 | WINNIE     | SNOW        | 2015-01-07 16:32:26.948243+00
     109695 | DYLAN      | HERRERA     | 2015-01-07 16:32:26.866374+00
     109694 | MARGARITA  | PENA        | 2015-01-07 16:32:26.774179+00
     109693 | BRET       | GILMORE     | 2015-01-07 16:32:26.695402+00
     109692 | SANDY      | MUELLER     | 2015-01-07 16:32:26.615914+00
     109691 | LUIS       | HUNTER      | 2015-01-07 16:32:26.537049+00
     109690 | SALLIE     | WELCH       | 2015-01-07 16:32:26.43215+00
    (10 rows)

And unaligned:

    loadtest=> <b>\a</b>
    Output format is unaligned.
    loadtest=> select id, first_name, last_name, date_joined from auth_user order by id desc limit 10;
    id|first_name|last_name|date_joined
    109699|LILLIE|CHRISTENSEN|2015-01-07 16:32:27.204538+00
    109698|VERA|WOLF|2015-01-07 16:32:27.111546+00
    109697|MARCO|BENSON|2015-01-07 16:32:27.028772+00
    109696|WINNIE|SNOW|2015-01-07 16:32:26.948243+00
    109695|DYLAN|HERRERA|2015-01-07 16:32:26.866374+00
    109694|MARGARITA|PENA|2015-01-07 16:32:26.774179+00
    109693|BRET|GILMORE|2015-01-07 16:32:26.695402+00
    109692|SANDY|MUELLER|2015-01-07 16:32:26.615914+00
    109691|LUIS|HUNTER|2015-01-07 16:32:26.537049+00
    109690|SALLIE|WELCH|2015-01-07 16:32:26.43215+00
    (10 rows)

Next, you probably want to use something other than a `|` as a delimiter; your
CSV pipline might not work with it well since it's a special character in
regular expressions. So replace it:

    loadtest=> <b>\f ','</b>
    Field separator is ",".

You can also use tabs, which I like because there's never (well, almost never)
a question about a tab being in the data:

    loadtest=> <b>\f '\t'</b>
    Field separator is "    ".
    loadtest=> select id, first_name, last_name, date_joined from auth_user order by id desc limit 10;
    id	first_name	last_name	date_joined
    109699	LILLIE	CHRISTENSEN	2015-01-07 16:32:27.204538+00
    109698	VERA	WOLF	2015-01-07 16:32:27.111546+00
    109697	MARCO	BENSON	2015-01-07 16:32:27.028772+00
    109696	WINNIE	SNOW	2015-01-07 16:32:26.948243+00
    109695	DYLAN	HERRERA	2015-01-07 16:32:26.866374+00
    109694	MARGARITA	PENA	2015-01-07 16:32:26.774179+00
    109693	BRET	GILMORE	2015-01-07 16:32:26.695402+00
    109692	SANDY	MUELLER	2015-01-07 16:32:26.615914+00
    109691	LUIS	HUNTER	2015-01-07 16:32:26.537049+00
    109690	SALLIE	WELCH	2015-01-07 16:32:26.43215+00
    (10 rows)

Next, you'll want to get rid of that `(10 rows)` line. In `psql` lingo that's
toggling the footer, which you do with the grab-bag `\pset` command:

    loadtest=> <b>\pset footer</b>
    Default footer is off.
    loadtest=> select id, first_name, last_name, date_joined from auth_user order by id desc limit 10;
    id	first_name	last_name	date_joined
    109699	LILLIE	CHRISTENSEN	2015-01-07 16:32:27.204538+00
    109698	VERA	WOLF	2015-01-07 16:32:27.111546+00
    109697	MARCO	BENSON	2015-01-07 16:32:27.028772+00
    109696	WINNIE	SNOW	2015-01-07 16:32:26.948243+00
    109695	DYLAN	HERRERA	2015-01-07 16:32:26.866374+00
    109694	MARGARITA	PENA	2015-01-07 16:32:26.774179+00
    109693	BRET	GILMORE	2015-01-07 16:32:26.695402+00
    109692	SANDY	MUELLER	2015-01-07 16:32:26.615914+00
    109691	LUIS	HUNTER	2015-01-07 16:32:26.537049+00
    109690	SALLIE	WELCH	2015-01-07 16:32:26.43215+00

Running that again will turn the footer back on.

Next, date formats. Some spreadsheets (like Google) don't like the default
timestamp format output by Postgres. You can put it into an ISO-8601 format
with the `to_char` function, which you can test out with the current time:

    loadtest=> SELECT to_char(CURRENT_TIMESTAMP, 'yyyy-MM-dd"T"HH24:MI:SS.MS');

Finally, instead of copy-n-pasting the output you'll want to send it directly
to a file. You can do that with '\o', as in:

    loadtest=> <b>\o my-output.csv</b>

You'll get no confirmation, and the output of **every** command you run will be
piped to the file. So now when you run:

    loadtest=> select id, first_name, last_name, to_char(date_joined, 'yyyy-MM-dd"T"HH24:MI:SS.MS') as date_joined
    loadtest->   from auth_user order by id desc limit 10;

And then toggle off the output to file:

    loadtest=> <b>\o</b>

You can open up the file `my-output.csv` and see something like this:

    id	first_name	last_name	to_char
    109699	LILLIE	CHRISTENSEN	2015-01-07T16:32:27.204
    109698	VERA	WOLF	2015-01-07T16:32:27.111
    109697	MARCO	BENSON	2015-01-07T16:32:27.028
    109696	WINNIE	SNOW	2015-01-07T16:32:26.948
    109695	DYLAN	HERRERA	2015-01-07T16:32:26.866
    109694	MARGARITA	PENA	2015-01-07T16:32:26.774
    109693	BRET	GILMORE	2015-01-07T16:32:26.695
    109692	SANDY	MUELLER	2015-01-07T16:32:26.615
    109691	LUIS	HUNTER	2015-01-07T16:32:26.537
    109690	SALLIE	WELCH	2015-01-07T16:32:26.432

Which Google Docs will happily import for you without fuss.

## Same but from CLI

The above examples are all using the shell. What if you want to do this from a
script?

Say we have a file `some_users.sql` with our query. And further say we want to
run it with a custom parameter every time -- like a date floor, represented by
`%AFTER%` in the text of the SQL. We can do something like this:

    #!/bin/bash -u

    PG=$1
    AFTER_DATE=$2

    cat some_users.sql | sed "s/%AFTER%/$AFTER_DATE/" | psql --no-align --pset footer --field-separator $'\t' -o some_users.csv $PG

which would be run like:

    ./some_users.sh postgres://.../mydb '2015-01-21 18:45:00'

and after it's run we'd have the `some_users.csv` file populated with the results.



