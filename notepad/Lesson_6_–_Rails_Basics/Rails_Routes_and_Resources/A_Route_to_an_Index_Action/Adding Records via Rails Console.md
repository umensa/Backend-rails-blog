# Adding Records via Rails Console
We've created a Page model class, but our list of pages is still blank.
Part of the problem is that no "Page" records exist now.
Let's go to the Rails console and fix that.

## Student's Notes
> page = Page.new
> page.title = "About This Blog"
> page.body = "Here I'll share my notes about Rails"
> page.slug = "about"
> page.save
