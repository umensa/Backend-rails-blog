# Has Many Associations
Let's add a Comment model now, and then set up an association so we can add Comments to a Post.

## Teacher's Notes

   * Let's add a Comment model now. 
   We'll give it a content attribute with a type of text to hold all the nice things our commenters have to say, and a name attribute with a type of string so we know who left it.
   `bin/rails g model Comment content:text name:string`

   * Don't forget to run `bin/rails db:migrate`.
   That will add a comments table with our content column to the database.
   * Now, we need a Post to add comments to. `post = Post.last`
   * post.comments fails with NoMethodError: undefined method 'comments' for #<Post...>
   * Add has_many :comments to Post.
       - This takes the symbol you specify, `:comments`, and add a method with that same name to all Post model objects.
       - Unlike with the Rails server, though, changes to your code aren't immediately available in the console.
       We need to exit the console first, then restart it with bin/rails c again.
   * Now we should be able to call our new comments method.
   `post = Post.last; post.comments`
       - Active Record attempts query SELECT "comments".* FROM "comments" WHERE "comments"."post_id" = ?
       - Error: no such column: comments.post_id

Active Record is looking for a column in the database that will allow it to associate comments with a Post.
We need to add the appropriate column.
But what table should we add it on?
The first thing you might attempt is to add several columns to the posts table, each holding the ID of a record from the comments table.
But you remember the time we considered adding the comment text to the posts table directly?
We rejected that idea because no matter what number of columns we added, it would be too few in some cases, and too many in others.
And this setup would give us the same problem.

So instead, we'll add a column on the comments table, where each record will hold the ID of a record from the posts table.
All the comments with a post_id of 1 will refer back to the record with an id of 1 in the posts table.
Comments with a post_id of 3 will refer back to the post with an id of 3.
Comments with a post_id of 7 will refer to the post with an id of 7.
And so on.

This is a common practice in database design, and is known as adding a foreign key column to a table.
The values that a column holds have to match the value of a primary key column, that is, the column that uniquely identifies a record, in a foreign table.
In this case, the post_id field in the comments table is a foreign key because it refers to values in the id column of the posts table, which is that table's primary key. 

	
   * `bin/rails generate migration AddPostToComments post_id:integer:index`
       - The index suffix will add an add_index method call to the migration.
       add_index causes a database table to be indexed by a particular field, in this case the post_id field.
       Now, when we need to look up records with a particular post_id in the comments table, our database won't have to look through the records one by one.
       Instead, it will just consult the index, which will point directly to all the records with the post_id we're looking for.
       Whenever you add a foreign key column to a table, you'll usually want to add an index on that column too, for speed's sake.

`class AddPostToComments < ActiveRecord::Migration[5.0]
  def change
    add_column :comments, :post_id, :integer
    add_index :comments, :post_id
  end
end`

   * post = Post.first (You could also use Post.last, Post.find, or any other method that gets you a single Post model object.)
   * post.comments returns an empty list right now.
   * To create a comment that's associated with a post:
       - comment = post.comments.build
       - comment.content = "Comment on first post"
       - comment.name = "Jay"
       - comment.save
       - post.comments now returns a list that includes our new comment.
   * To create a comment and save it immediately:
       - post.comments.create(content: "Cool!", name: "Alena")
       - Added to list returned from post.comments.
   * To create and view comments on different post:
       - post = Post.last
       - post.comments.create(content: "Comment on last post", name: "Pasan")
       - Post.last.comments
       - Post.first.comments
       - Comment.all

## Student's Notes

> bin/rails c

> post = Post.last
	=> nil
> post.comments
	=> undefined

__app/models/post.rb__
class Post < ApplicationRecord
  has_many :comments
end

> post.comments
	=> ActiveRecord::StatementInvalid (SQLite3::SQLException: no such column: comments.post_id: SELECT "comments".* FROM "comments" WHERE "comments"."post_id" = ?)

> bin/rails g migration AddPostToComments post_id:integer:index

__db/migrate/20210503******_add_post_to_comments.rb__
class AddPostToComments < ActiveRecord::Migration[5.0]
  def change
    add_column :comments, :post_id, :integer
    add_index :comments, :post_id
  end
end

> bin/rails db:migrate

> bin/rails c

   > post = Post.first
   > post.comments
   	Comment Load (0.3ms)  SELECT "comments".* FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 1]]
	=> #<ActiveRecord::Associations::CollectionProxy []>
   > comment = post.comments.build
   > comment.content = "Comment on first post"
   > comment.save
   > post.comments
   > post.comments.create(content: "Cool!", name: "Alena")
   > pp post.comments
[#<Comment:0x00005642c0b20be8
  id: 1,
  content: "Comment on first post",
  name: "Jay",
  created_at: Mon, 03 May 2021 20:41:26 UTC +00:00,
  updated_at: Mon, 03 May 2021 20:41:26 UTC +00:00,
  post_id: 1>,
 #<Comment:0x00005642c099b5c0
  id: 2,
  content: "Cool!",
  name: "Alena",
  created_at: Mon, 03 May 2021 21:06:38 UTC +00:00,
  updated_at: Mon, 03 May 2021 21:06:38 UTC +00:00,
  post_id: 1>]
=> #<ActiveRecord::Associations::CollectionProxy [#<Comment id: 1, content: "Comment on first post", name: "Jay", created_at: "2021-05-03 20:41:26", updated_at: "2021-05-03 20:41:26", post_id: 1>, #<Comment id: 2, content: "Cool!", name: "Alena", created_at: "2021-05-03 21:06:38", updated_at: "2021-05-03 21:06:38", post_id: 1>]>
   > post = Post.last
   > post.comments.create(content: "Comment on last post", name: "Pasan")
   > pp Post.last.comments

# Has Many

**Challenge Task 1 of 1**
We're working on an application for a veterinarian's office. Update this Owner model class to specify that an Owner "has many" instances of the Pet model.

__models/owner.rb__
class Owner < ApplicationRecord
	has_many :pets
end

# Association Methods

**Challenge Task 1 of 1**

We've loaded a Rails environment that includes a Pet model class and an Owner model class which has_many :pets. Code that you type here in playground.rb will work just like the code we've been demonstrating in the Rails console.

Load the first Owner from the database. Then, create a new Pet belonging to that Owner. Set the Pet's name attribute to any string you want, and ensure the Pet is saved to the database.

__playground.rb__
first = Owner.first
first.pets.create(name: "sweety")
first.save

# A "Has Many" Migration

**Challenge Task 1 of 1**

Assume that a pets table already exists. Here at the command line, generate a migration that will add an owner_id foreign key column to the pets table.

> bin/rails g migration AddOwnerToPets owner_id:integer:index
