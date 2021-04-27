#Rails Console: Creating Model Object
Since reading from the database is easiest, we'll go a little bit out of order in our tour of CRUD operations, and start with "read" operations.

##Techer's Notes

We can create new records in the database by creating new model objects, setting their attributes, and saving them.

   * We can create a new Post object by calling `Post.new`. We can create a new "Post" and assign it to a variable: `post = Post.new`
   * You can see the object we got in the Rails console output. Notice that its attributes are all set to "nil": `#<Post id: nil, title: nil, created_at: nil, updated_at: nil>`
   * You can set the attributes the same way you would on any other Ruby object. Let's assign a title for this new Post: `post.title = "Hello, console!"`
   * To store it in the database, we need to call the "save" method on the object: `post.save`.
   * We'll see an SQL query that inserts a new post into the "posts" table, with the "title" we assigned: `INSERT INTO "posts" ("title", "created_at", "updated_at") VALUES (?, ?, ?) [["title", "Hello, console!"], ["created_at", 2016-07-13 19:50:08 UTC], ["updated_at", 2016-07-13 19:50:08 UTC]]`

Every model object you save to the database gets a value written to its id database column. Notice that our Post object didn't have an id when we first created it.

   * If we look at the Post after saving it, we'll see it's been assigned one: `#<Post id: 7, title: "Hello, console!", created_at: "2016-07-13 19:50:08", updated_at: "2016-07-13 19:50:08">`
   * As we saw before, you can pass an object's id to the find method to look it back up later: `Post.find(7)`

**Frequently Asked Questions**

Q: In the console, I created a Post with Post.new, but when I type post.title = "some value" I get `undefined local variable or method 'post'`! What's going on?

A: Calling Post.new doesn't automatically assign it to a variable; the post variable doesn't exist until you assign a value to it. Be sure to assign the new Post to a variable with `post = Post.new`.
