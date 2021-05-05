#Rails Console: Deleting Model Objects
We'll end our tour of the Rails console with "delete" operations.

##Techer's Notes

Your users need to be able to delete data as well, so Rails also allows the removal of records from the database. We just load up a particular instance of the model, as before, and then call the "destroy" method on it.

   * As before, we can load a particular instance using its ID, and assign it to a variable: `post = Post.find(7)`
   * Now, we'll call the "destroy" method on that object: `post.destroy`.
   * We'll see an SQL query that deletes the record from the database.
