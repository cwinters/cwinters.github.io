---
title: "Recipe for using sqitch on Codeship"
layout: post
tags: "database continuousintegration perl"
---

The [sqitch](http://sqitch.org) tool is a standaone database migration tool not
tied to any language. It doesn't try and sync models with your database, or
assume that it should be managing everything in your database, or generally
stick its fingers where they don't belong.

David Wheeler (the author) has put a ton of work into making instatllation
straightforward, as evidenced by the substantial list of
installation alternatives (`cpan` and `cpanm`, `apt-get`, `homebrew`, `yum`) on
the homepage.

However the linux-based ones assume you've got `sudo` rights, and that's not
true on CI services like Codeship. Here are the steps I went through to make
`sqitch` available for my tests:

__1. Test settings__

Most of the work is done here.

The first step is to download and install
[cpanminus](http://search.cpan.org/dist/App-cpanminus/) because the default
`cpan` isn't as amenable to one-time automated use.
<sup id="sqitch-fnref:1"><a href="#sqitch-fn:1" rel="footnote">1</a></sup>

    pushd ~/bin
    curl -L https://cpanmin.us/ -o cpanm
    chmod +x cpanm
    popd

Yes, this is downloading a script directly from the internet. It's one that's
auto-generated from the module's source, and the author is very well known and
regarded. If we were paranoid we could download the script ourselves and put it
on a server we control.

Next we need to install `sqitch`. We're using Postgres so in addition to
installing the module itself we're installing the Perl-to-Postgres database
interface:

    ~/bin/cpanm --notest App::Sqitch DBI DBD::Pg

Finally we need to modify the path and tell Perl where these additional
libraries are stored. The output of the above step starts with this banner:

    ! Can't write to /usr/local/share/perl/5.18.2 and /usr/local/bin: Installing modules to /home/rof/perl5
    ! To turn off this warning, you have to do one of the following:
    !   - run me as a root or with --sudo option (to install to /usr/local/share/perl/5.18.2 and /usr/local/bin)
    !   - Configure local::lib your existing local::lib in this shell to set PERL_MM_OPT etc.
    !   - Install local::lib by running the following commands
    !
    !         cpanm --local-lib=~/perl5 local::lib && eval $(perl -I ~/perl5/lib/perl5/ -Mlocal::lib)

The very end of that first line tells us the path where our modules will be
installed. (It's Codeship-specific, but AFAIK it's stable from
project-to-project.) We'll need to include that in the path and library
setting. With those environment variables here's what the full test settings
look like (in an easy copy-paste block):

    # install cpanminus
    mkdir -p ~/bin
    pushd ~/bin
    curl -L https://cpanmin.us/ -o cpanm
    chmod +x cpanm
    popd
    
    # install sqitch and postgres interface
    ~/bin/cpanm --notest App::Sqitch DBI DBD::Pg
    
    # make sqitch and libraries available
    export PATH=/home/rof/perl5/bin:$PATH
    export PERL5LIB=/home/rof/perl5/lib/perl5

__2. Your test script__

We have a standard `test.sh` script at the root of every project. It doesn't do
a whole lot, but it gives us a place to put CI-specific configuration. In the
Codeship case the only thing we need to change is the port.
<sup id="sqitch-fnref:2"><a href="#sqitch-fn:2" rel="footnote">2</a></sup>
Since we're using 9.4-specific features we set it to 5434. Here's the setup we
do to create a database and deploy migrations with sqitch:

    #!/bin/bash
    
    DATABASE_NAME="myproject_test"
    
    PORT=5432
    if [ "$CI" = "true" ]; then
      PORT=5434
    fi
    DB_COUNT=`psql --port $PORT -l | grep -c "$DATABASE_NAME "`
    if [ $DB_COUNT -eq 0 ]; then
      echo "Database does not exist, creating..."
      psql --port $PORT -c "CREATE DATABASE $DATABASE_NAME" postgres
    fi
    
    sqitch deploy db:pg://localhost:$PORT/$DATABASE_NAME
    if [ $? -ne 0 ]; then
      echo "Sqitch migration FAILED. Refusing to run tests."
      echo "Dropping database for clean next run."
      psql --port $PORT -c "DROP DATABASE $DATABASE_NAME" postgres
      exit 1
    fi
    echo "Database setup done. Run tests..."
    ...

__3. Profit!__

A successful test output now starts with something like this
(individual migration names depend on your project, of course):

    Database does not exist, creating...
    CREATE DATABASE
    Adding registry tables to db:pg://localhost:5434/myproject_test
    Deploying changes to db:pg://localhost:5434/myproject_test
    + ltree ........ ok
    + groups ....... ok
    + memberships .. ok
    + activities ... ok
    Database setup done. Run tests...

Go forth and migrate!

<div class="footnotes">
<ol>
  <li class="footnote" id="sqitch-fn:1">
    There are many tips -- like
    <a href="http://stackoverflow.com/questions/3462058/how-do-i-automate-cpan-configuration">this one from SO</a>
    -- on generating an automation-friendly config for CPAN, but
    they seem to be geared toward making tasks automatable for
    convenience rather than necessity.
    <a href="#sqitch-fnref:1" title="return to article"></a>
  </li>
  <li class="footnote" id="sqitch-fn:2">
    <a href="https://codeship.com/documentation/databases/postgresql/">Codeship runs</a>
    different versions of Postgres on different ports, which is a pretty
    elegant solution IMO.
    <a href="#sqitch-fnref:2" title="return to article"></a>
  </li>
</ol>
</div>
