# Build me a website

See how it works locally:

    $ jekyll serve
    Notice: for 10x faster LSI support, please install http://rb-gsl.rubyforge.org/
    Configuration file: /Users/c.winters/Projects/github/cwinters.github.io/_config.yml
                Source: /Users/c.winters/Projects/github/cwinters.github.io
           Destination: /Users/c.winters/Projects/github/cwinters.github.io/_site
          Generating...
                        done.
    Configuration file: /Users/c.winters/Projects/github/cwinters.github.io/_config.yml
        Server address: http://0.0.0.0:4000/
      Server running... press ctrl-c to stop.

Editing:

1. Create doc in `_drafts` with no date.
2. Write write write.
3. `git mv _drafts/howard_the_duck_is_awesome.md _posts/2016-07-08-howard_the_duck_is_awesome.md`
4. Commit and push, then wait...

Go forth and write!

## Notes

### Related posts

Originally the `_layouts/post.html` had this at the bottom:

    <div id="related">
      <h3>Related posts</h3>
      <ul class="posts">
        {% for post in site.related_posts limit:3 %}
        <li>
          <span>{{ post.date | date_to_string }} &raquo;</span> <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
        {% endfor %}
      </ul>
    </div>

the problem is that `site.related_posts` doesn't actually work. Even
being able to pick a handful of random ones would be cool. But no dice...

