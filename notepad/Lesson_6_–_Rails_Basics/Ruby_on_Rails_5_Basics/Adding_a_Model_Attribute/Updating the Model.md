#Updating the Model
Our app is able to store titles for our posts, but we forgot to add a post body to hold the actual post content.
In this stage, we're going to fix that.

##Techer's Notes

Any time we want to update a Rails database, we need to use a migration.
And to create that, we'll need the "rails generate" command:

`rails generate migration AddBodyToPosts body:text`

   * The migration to create the "posts" table was set up as part of the scaffold we used earlier.
   This time, we'll need to create the migration separately.
   So instead of the "scaffold" generator, we're going to run the "migration" generator.
   * Next is the migration name.
   It should be in CamelCase (with each word capitalized), since it will be used as a class name.
   * We can name the migration whatever we want, but if it's in the form `Add<attribute name>To<table name>`, the generator will set up a command to add a column to that table for us.
   So we name it "AddBodyToPosts".
   * Next we can specify one or more columns we want to add, just like we did when generating the scaffold before.
   * Here we specify "body:text" to create a "body" attribute of type "text".
   * Previously, for the title, we used a type of "string". But the post body needs to be longer, so we use a type of "text" here, so that the resulting database column can hold more text.

Don't forget, generating the migration doesn't actually update the database. To do that, run `bin/rails db:migrate`.

**Frequently Asked Questions**

Q: In the console, I loaded a Post with Post.first, but when I type `post.body = "some value"` I get `undefined local variable or method 'post'`! What's going on?

A: Calling the Post.first method doesn't automatically assign it to a variable; the post variable doesn't exist until you assign a value to it. Be sure to assign the return value of Post.first to a variable with `post = Post.first`.
