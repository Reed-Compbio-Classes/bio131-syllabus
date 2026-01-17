# Bio131 Syllabus

This is the content for Reed College's Bio131, taught by Anna Ritz. The website is live at this link:

[https://reed-compbio-classes.github.io/bio131-syllabus/](https://reed-compbio-classes.github.io/bio131-syllabus/)

### Developer Notes

**To run locally:** tested with Ruby 3.4.3 and jekyll 4.3.3. You might have to do `bundle install` or `bundle update` before serving the website locally.

```
bundle exec jekyll serve
```

**To pass GitHub actions:** if you change the `Gemfile`, you need to `bundle update` to get the additional gems installed. This changes the `Gemfile.lock` file. If you commit the lock file, you need to add the linux platform to it so GitHub actions work and the website is deployed without error:

```
 /usr/local/opt/ruby/bin/bundle lock --normalize-platforms
```

(Note: as of 1/17/25 I installed a newer version of ruby using `homebrew`, needed to call `/usr/local/opt/ruby/bin/bundle`)

**To get relative links:** I had to add the `jekyll-relative-links` gem to the Gemfile (this should be distributed with GitHub pages, but it didn't work with just-the-docs template).

**For tests to pass in GitHub Actions (1/17/2026):** I had to downgrade Ruby to 3 for GitHub Actions. From the ChatGPT solution (which worked):

This failure is happening because your workflow is asking ruby/setup-ruby to install Ruby 3.4 on ubuntu-24.04, but the action’s prebuilt Rubies for that runner image currently only go up to 3.3.x (exactly what the error list shows). On top of that, your stack trace shows the action is being used via a pinned commit hash (.../_actions/ruby/setup-ruby/857595...), and the action itself warns you to use ruby/setup-ruby@v1 instead.

Update your Pages workflow so it:

1. uses ruby/setup-ruby@v1 (not a pinned SHA), and
2. uses Ruby 3.3 (available on ubuntu-24.04 per your error output)

In .github/workflows/pages.yml (or whatever your Pages workflow file is named), change the Ruby step to something like:

```
- name: Setup Ruby
  uses: ruby/setup-ruby@v1
  with:
    ruby-version: '3.3'
    bundler-cache: true
```

That should get the action unstuck immediately, while keeping you on the current GitHub runner image.