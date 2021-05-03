#Rails Console: Reading Model Objects
Since reading from the database is easiest, we'll go a little bit out of order in our tour of CRUD operations, and start with "read" operations.

##Techer's Notes


We can get a collection of all of the "Post" objects in our database by calling the "all" method on the "Post" class. We can type "Post.all" at the prompt...

   * We'll see this SQL query: "Post Load (0.2ms) SELECT "posts".* FROM "posts"", just like we saw when "Post.all" was called from our posts controller earlier.
   * Then, the Rails console displays the return value of that method call, the collection of all "Post" objects: `=> #<ActiveRecord::Relation [#<Post id: 1, title: "Hello, Rails!", created_at: "2016-05-28 18:21:19", updated_at: "2016-05-28 18:21:19">, #<Post id: 3, title: "Second post", created_at: "2016-05-28 23:04:35", updated_at: "2016-05-28 23:04:35">]>`

We can get back just the most recent "Post" object by calling the "last" method on the "Post" class. If we type "Post.last" at the prompt...

   * We'll see the same SQL query that was generated for "Post.all", but limited to just one record: "Post Load (0.1ms) SELECT "posts".* FROM "posts" ORDER BY "posts"."id" DESC LIMIT ? [["LIMIT", 1]]".
   * The return value consists of just one "Post" model object: `#<Post id: 3, title: "Second post", created_at: "2016-05-28 23:04:35", updated_at: "2016-05-28 23:04:35">`

Notice that each model object has had a value automatically assigned to its "id" database column. We can pass that ID to the "find" class method to load a particular record from the database.

   * The last "Post" object here has an ID of 3. We can type "Post.find(3)"...
   * We'll see the SQL query `SELECT "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT ? [["id", 1], ["LIMIT", 1]]`. This query is limited to just one database row, the one with an ID matching the ID we specified.
   * The return value again consists of just one "Post" object, the one whose ID matched: 
   `#<Post id: [??], title: "Hello, Rails!", created_at: "2016-07-07 22:53:46", updated_at: "2016-07-07 22:53:46">`
