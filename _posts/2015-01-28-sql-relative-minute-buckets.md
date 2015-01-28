---
title: "Creating buckets for relative minutes in SQL"
tags: "sql database postgres"
layout: post
---

Aggregating use over buckets of time is really useful when doing performance
testing. For example, if you have a script that throws a bunch of requests at
your system in a known time series you can re-run that script to gauge the
effectiveness of your changes. So say we have a table:

{% highlight sql %}
CREATE TABLE tasks (
  id         INT        NOT NULL,
  task_type  VARCHAR(8) NOT NULL,
  created    TIMESTAMP  NOT NULL,
  completed  TIMESTAMP,
  operations INT,
  PRIMARY KEY(id)
);
{% endhighlight %}

and we know the tasks we're interested in aggregating were created between
23:41 and 23:51. We can do the following in Postgres to aggregate the
operations into buckets by creation minute so we can show the average elapsed
time:

{% highlight sql %}
WITH offsets AS (
  SELECT
    (EXTRACT(minute FROM created) || ' minutes '
    || EXTRACT(second FROM created) || ' seconds')::interval AS initial
  FROM
    tasks
  WHERE
    created BETWEEN '2015-01-27 23:41' AND '2015-01-27 23:51'
  ORDER BY
    created
  LIMIT
    1
),
summary AS (
  SELECT
    id,
    task_type,
    operations,
    created,
    EXTRACT(minute FROM (created - offsets.initial)) AS created_minute,
    completed,
    EXTRACT(minute FROM (completed - offsets.initial)) AS completed_minute,
    EXTRACT(milliseconds FROM completed - created) AS elapsed
  FROM
    tasks, offsets
  WHERE
    created BETWEEN '2015-01-27 23:41' AND '2015-01-27 23:51'
)
SELECT
  created_minute,
  COUNT(*) AS num_created,
  ROUND(AVG(elapsed)::numeric, 1) AS avg_elapsed
FROM
  summary
GROUP BY
  created_minute
ORDER BY
  created_minute;
{% endhighlight %}

It seems long and your eyes might glaze over, but there are two interesting
parts. The first
[CTE](http://www.postgresql.org/docs/9.3/static/queries-with.html) named
`offsets` finds the first row in our dataset and constructs a string
representing the minutes and seconds, then casts it to an interval. 
So if our first row had a creation date of `2015-01-27 23:41:18.867530` the
text of the interval would be `41 minutes 18.867530 seconds`, which Postgres
will display as `00:41:18.867530`. You can test this without a table just by
extracting the interval from `NOW()`:

{% highlight sql %}
SELECT
  (EXTRACT(minute FROM NOW()) || ' minutes'
  || ' '
  || EXTRACT(second FROM NOW()) || ' seconds')::interval;
{% endhighlight %}

and get a result with something like:

        interval
    -----------------
     00:33:56.694513

In the next CTE (`summary`), we'll join to that one-row table containing an
interval to give us something to subtract from our data before extracting a
minute. So applying this interval to our first row would do:

    2015-01-27 23:41:18
             - 00:41:18
    ===================
    2015-01-27 23:00:00

and applying it to another row in the dataset might do:

    2015-01-27 23:48:08
             - 00:41:18
    ===================
    2015-01-27 23:06:50

and we'd `EXTRACT` the minute from the first row as `0`, from the other row as
`6`.

Finally is our actual `SELECT`: we've got the minute bucket and elapsed time
for each row we can do some simple aggregation (a count and average) grouping
by the bucket. Piece of cake!

