---
title: "Today I learned: Bash and Ansible"
tags: bash shell programming
layout: post
---

### Iterating through strings

Bash guides ([like this](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-7.html))
typically talk about arrays in terms of globs. Makes sense, since that's a really common use.

But sometimes you want to be able to iterate through plain old strings, like
this where we iterate through three words and for each of those iterate through
two others so we can generate some commands:

{% highlight bash %}
if [ $DIRECTION == "delete" ]; then
  for node in API Web Worker; do
    for action in daily-spinup daily-spindown; do
      aws autoscaling delete-scheduled-action --auto-scaling-group-name ${AWS_ENV}${node} --scheduled-action-name $action
    done
  done
fi
{% endhighlight %}

which will wind up generating six commands, assuming `AWS_ENV=qa`:

{% highlight bash %}
aws autoscaling delete-scheduled-action --auto-scaling-group-name qaAPI --scheduled-action-name daily-spinup
aws autoscaling delete-scheduled-action --auto-scaling-group-name qaAPI --scheduled-action-name daily-spindown
aws autoscaling delete-scheduled-action --auto-scaling-group-name qaWeb --scheduled-action-name daily-spinup
aws autoscaling delete-scheduled-action --auto-scaling-group-name qaWeb --scheduled-action-name daily-spindown
aws autoscaling delete-scheduled-action --auto-scaling-group-name qaWorker --scheduled-action-name daily-spinup
aws autoscaling delete-scheduled-action --auto-scaling-group-name qaWorker --scheduled-action-name daily-spindown
{% endhighlight %}

[This doc](http://tldp.org/LDP/abs/html/loops1.html) has a lot of good examples.

### Refreshing Ansible's EC2 cache

Bringing environments up and down every day means that Ansible's EC2 cache can
get invalid much quicker. You can invalidate it, and check the results, with:

{% highlight bash %}
$ ./ec2.py --refresh-cache
{
  "_meta": {
    "hostvars": {
   ... loads of JSON ...
    }
}

$ ls -al ~/.ansible/tmp/
ubuntu@ip-10-3-81-9:~$ ls -al ~/.ansible/tmp/
total 72
drwxrwxr-x 4 ubuntu ubuntu  4096 Jan  9 01:22 .
drwxrwxr-x 4 ubuntu ubuntu  4096 Jul  7  2014 ..
-rw-rw-r-- 1 ubuntu ubuntu 49794 Jan  9 14:54 ansible-ec2.cache
-rw-rw-r-- 1 ubuntu ubuntu  1170 Jan  9 14:54 ansible-ec2.index
...
{% endhighlight %}

as mentioned 
[in the docs](http://docs.ansible.com/intro_dynamic_inventory.html#example-aws-ec2-external-inventory-script).

