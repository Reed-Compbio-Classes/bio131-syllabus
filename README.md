# Bio131 Syllabus

This is the content for Reed College's Bio131, taught by Anna Ritz. The website is live at this link:

[https://reed-compbio-classes.github.io/bio131-syllabus/](https://reed-compbio-classes.github.io/bio131-syllabus/)

### Developer Notes

**To run locally:** tested with Ruby 3.4.3 and jekyll 4.3.3. You might have to do `bundle install` or `bundle update` before serving the website locally.

```
bundle exec jekyll serve
```

**To pass GitHub actions:** if you change the `Gemfile`, you need to `bundle update` to get the addtional gems installed. This changes the `Gemfile.lock` file. If you commit the lock file, you need to add the linux platform to it so GitHub actions work and the website is deployed without error:

```
 /usr/local/opt/ruby/bin/bundle lock --normalize-platforms
```

(Note: as of 1/17/25 I installed a newer version of ruby using `homebrew`, needed to call `/usr/local/opt/ruby/bin/bundle`)

**To get relative links:** I had to add the `jekyll-relative-links` gem to the Gemfile (this should be distributed with GitHub pages, but it didn't work with just-the-docs template).