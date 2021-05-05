#Rails Console: Updating Model Objects
Next let's look at "update" operations in the console.

##Techer's Notes

After retrieving a model object from the database, we can modify its data and update the database record. This is much the same as working with a new model object; we just assign new values to the existing object's attributes, and call "save" on it.

Let's suppose we wanted to update a posts's title:

   * As before, we can get a collection of all the Post objects by calling `Post.all`.
   * We can look at the "id" attribute of the one we want to update, and then retrieve it by passing the ID to the "find" method. We'll assign the object we get back to a variable: `post = Post.find(7)`
   * As before, we can set the attributes the same way we would on any other Ruby object. So let's change the title: `post.title = "I've been updated!"`
   * Once again, these changes only exist in your computer's memory, not in the database. We need to call the "save" method on the object to save it to the database: `post.save`
