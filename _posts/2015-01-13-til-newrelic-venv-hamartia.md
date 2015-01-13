---
title: "Today I learned: newrelic-admin + venv, and hamartia"
layout: "post"
tags: python newrelic monitoring vocabulary
---

## NewRelic + Virtualenv = Happy

The [configuration docs](https://docs.newrelic.com/docs/agents/python-agent/installation-configuration/python-agent-integration)
clearly state:

> The newrelic-admin program you run must be coming from the same Python
> installation or virtual environment as your application is using. You cannot
> mix programs/components from different Python installations. If this is done,
> the agent will not run correctly.)

it's just when I read those back in November I didn't understand well what
[Virtual Environments](http://docs.python-guide.org/en/latest/dev/virtualenvs/)
are in Python. Now I understand a little bit more, but it's still feels of
magic though I know it's a SMOP behind the scenes.

Anyway, since we we're using Supervisor we'd been starting up the processes
like this:

    [program:awesomeo-5000]
    user=ubuntu
    command=/usr/local/bin/newrelic-admin run-program /usr/local/bin/awesomeo --model 5000
    directory=/opt/awesomeo
    environment=
        ...
        CACHE_SERVER="{{ cache_server }}",
        NEW_RELIC_CONFIG_FILE="/opt/awesomeo/newrelic.ini"

but since the program we're running had its own virtual environment
`newrelic-admin` would silently fail. Our program would start up just fine, but
no monitoring data would be sent. And, frustratingly, no logging data would be
written out -- even with this in the INI:

    [newrelic]
    ...
    log_file = /tmp/newrelic-agent.log
    log_level = debug

Re-installing the program with:

    $ source venv/bin/activate
    $ pip install -I newrelic

or the Ansible play:

    - name: lightbox API | force newrelic package into virtualenv
        pip:
          name=newrelic
          virtualenv={{ app_dir }}/venv
          virtualenv_site_packages=yes
          extra_args='-I'
          state=present
        sudo: False

will put it in your venv even if it's installed locally.

## New word: Hamartia

I ran across this word in a student essay today. It's a neat word, and I hadn't
seen how Google treats such terms, which I think is both useful and
informative:

![Google defines Hamartia](/images/blog/google_defines_hamartia.png)

...though the pronunciation icon didn't work for me. (shrug)


