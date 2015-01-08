---
title: "Today I learned: Django aggregate queries, auto scaling"
layout: post
tags: "orm query aws commandline"
---

## Django aggregate queries

I've been using Django, lightly, for a couple months now. It's generally fine,
pretty easy to find how to make things work. I'm not really fond of the ORM's
query capabilities. Some parts of it just look gross -- like if you're finding
an assignment with one of many IDs:

{% highlight python %}
assignments = Assignment.objects.filter(pk__in=my_ids).all()
{% endhighlight %}

I suppose it's a mark of how briefly I've been programming Python that the
double underscores still feel weird and look ugly. Completely subjective. And
I'm sure they (and other things) will grow on me, just like all syntaxes
eventually do.

Anyway, I hadn't done many aggregation queries so far. And my tendency is to
drop immediately to SQL because I know SQL pretty well, and it's nice to drop
into something comfy when so many other things are unfamiliar.

But in a recent PR comment my colleague had pointed out how the ORM's query
capabilities handled a slightly tricky case, and I figured I'd try to
investigate that more.  And like a lot of Django the docs are
[not only easy to find](https://docs.djangoproject.com/en/1.7/topics/db/aggregation/)
but also quite clear and chock full of examples. So I figured out in a 
flash that instead of something like:

{% highlight sql %}
  SELECT student_id, MAX(created_at)
    FROM assignment_answers
   WHERE assignment_id = 7891
         AND final_submission
GROUP BY student_id
{% endhighlight %}

we can do it with code, and we'll get back a list of tuples:

{% highlight python %}
submitted_answers = assignment.answers.filter(final_submission=True)
all_submissions = submitted_answers.values_list('student_id').annotate(Max('created_at')).order_by()
{% endhighlight %}

Personally I think the SQL reads better, but some people find it jarring to see
SQL mixed in with code. So it's fine.

## Scheduling AWS Auto Scaling Events

I've been interested in bringing down a number of our environments in off
hours -- running them for 65 hours a week (5\*13) is a good bit cheaper than
running them for 168 (7\*24).

I figured this would be a bunch of work, but my colleague (same one as earlier,
one sharp guy) pointed me to
[the section of the docs](http://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/schedule_time.html)
that tells you exactly how to set this up. Scheduling these actions is not
available from the AWS Management Console (their web UI) and I'm still new
enough to AWS manipulation to not even know to look.

So once you have the [awscli](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)
package installed and configured, you can just do something like the following,
given an auto scaling group named 'qaAPI' that you want to take to 0 instances
at 1 AM UTC (8 PM our time) every day:

{% highlight bash %}
$ aws autoscaling put-scheduled-update-group-action \
    --auto-scaling-group-name qaAPI \
    --scheduled-action-name daily-spindown \
    --recurrence '0 1 * * *' \
    --min-size 0 --max-size 1 --desired-capacity 0
{% endhighlight %}

and then another one to bring them back up at 12 PM UTC (7 AM our time):

{% highlight bash %}
$ aws autoscaling put-scheduled-update-group-action \
    --auto-scaling-group-name qaAPI \
    --scheduled-action-name daily-spinup \
    --recurrence '0 12 * * *' \
    --min-size 1 --max-size 1 --desired-capacity 1
{% endhighlight %}

Since these don't show up in the web UI you'll probably want to check your work
with:

{% highlight bash %}
$ aws autoscaling describe-scheduled-actions \
    --auto-scaling-group-name qaAPI
{% endhighlight %}

Pay attention to the `start_time` attribute -- if it's set to tomorrow, you
probably forgot (as I did) that you're working in UTC.

Finally, I love that cron recurrence schedules are re-used for this, rather
than inventing something much more confusing and error-prone.

