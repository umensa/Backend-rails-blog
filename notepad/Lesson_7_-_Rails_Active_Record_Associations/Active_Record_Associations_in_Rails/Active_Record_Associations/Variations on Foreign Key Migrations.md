# Variations on Foreign Key Migrations
There are many ways to add the foreign key column that's required by our has_many and belongs_to associations, and I want to take a moment to show you a couple more of them.

## Teacher's Notes
There are many ways to add the foreign key column that's required by our has_many and belongs_to associations, and I want to take a moment to show you a couple more of them.

    If you want, you can use the references column type in migrations instead.
        bin/rails generate migration AddPostToComments post:references
        That will create a migration with a call to the add_reference method instead of add_column. add_reference takes a symbol with a table name, and a symbol with the name of a model to add a foreign key for. It'll create a column whose name begins with that model name, and ends in _id. And since it's always desirable to have an index on foreign key columns, add_reference will add an index as well. So add_reference :comments, :post will create a post_id column in the comments table just like add_column did, but it will also add an index on that column automatically.
        The foreign_key: true argument will set up a foreign key constraint on databases that support it.

class AddPostToComments < ActiveRecord::Migration[5.0]
  def change
    add_reference :comments, :post, foreign_key: true
  end
end

Without a foreign key constraint, we could create a comment with a post_id field set to 999, even if there was no record in the post table with an id of 999. With a foreign key constraint, the database would prevent such a record from even being saved. Foreign key constraints help keep bad data from sneaking into your database.

Note that the adapter for the SQLite database that Rails uses by default doesn't support foreign key constraints. Your migration will still work, and it's a good idea to get in the habit of adding the constraints in your migrations. But if you want the database to actually enforce the constraints, you'll need to switch to another database like MySQL or PostgreSQL.

    Using Rails with PostgreSQL (http://railscasts.com/episodes/342-migrating-to-postgresql?view=asciicast)
    Using Rails with MySQL (https://richonrails.com/articles/getting-started-with-mysql-and-ruby-on-rails)

If we know we're going to need an association when we're first creating a model, we can set the necessary columns up then, too.

    Let's re-generate the Comment model. We can replace the two migrations with a single migration that creates the comments table and adds a post_id column along with the other columns: rails g model Comment content:text name:string post:references.
        We can allow it to overwrite the existing model class file, as well as another file related to tests.
        Don't forget to run bin/rails db:migrate.
        We should now be able to create comments associated with a post again.

## Student's Notes

> bin/rails db:rollback

> bin/rails destroy migration AddPostToComments

> bin/rails g migration AddPostToComments post:references

__db/migrate/20210504******_add_post_to_comments.rb__
class AddPostToComments < ActiveRecord::Migration[5.0]
  def change
    add_reference :comments, :post, foreign_key: true
  end
end

> bin/rails db:migrate

> bin/rails c
   > Post.first.comments.create(content: "Hi", name: "Jay")
   > pp Post.first.comments

> ls db/migrate
> bin/rails db:rollback
> bin/rails db:rollback
> bin/rails destroy migration AddPostToComments
> bin/rails destroy migration CreateComments
> bin/rails g model Comment content:text name:string post:references
> bin/rails db:migrate

> bin/rails c
   > post = Post.first
   > post.comments.create(content: "Hi", name: "Alena")
   > pp Post.first.comments
