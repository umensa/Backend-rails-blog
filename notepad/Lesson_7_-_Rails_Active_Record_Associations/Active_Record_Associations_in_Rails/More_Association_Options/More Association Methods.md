# More Association Methods
There are more useful methods you can call on an association. We'd like to show you a few of these now.

## Teacher's Notes

There are more useful methods you can call on an association. We'd like to show you a few of these now.

Suppose we have a new Post that doesn't have any Comments yet. We can use the present? and empty? methods to check whether comments are present:

post = Post.create(title: "Newest post")
Post.last.comments
Post.last.comments.empty? # => true
Post.last.comments.present? # => false

Any method we can use in the Rails console can be used in a controller or view as well. The empty? or present? methods can be used to change what your view renders when a collection is empty.

    Only rendering <h1>Comments</h1> if comments present

views/posts/show.html.erb

  <% if @post.comments.present? %>
    <h1>Comments</h1>
    <%= render @post.comments %>
  <% end %>

The size method lets you check the number of records in a collection.

2.3.0 :001 > Post.first.comments
 => #<ActiveRecord::Associations::CollectionProxy [#<Comment id: 1, content: "Hi", name: "Alena", post_id: 1, created_at: "2017-10-02 01:01:33", updated_at: "2017-10-02 01:01:33">, #<Comment id: 2, content: "Nice post!", name: "Jay", post_id: 1, created_at: "2017-10-02 21:50:17", updated_at: "2017-10-02 21:50:17">, #<Comment id: 3, content: "Cool!", name: "Pasan", post_id: 1, created_at: "2017-10-02 21:50:34", updated_at: "2017-10-02 21:50:34">]>
2.3.0 :003 > Post.first.comments.size
 => 3

Active Record adds a where method to associations that allows you to further filter the set of results. For example, we've got comments on the first post from several different authors. If I wanted to limit that to comments where the name field was "Alena", I could write Post.first.comments.where(name: "Alena"):

2.3.0 :004 > Post.first.comments.where(name: "Alena")
 => #<ActiveRecord::AssociationRelation [#<Comment id: 1, content: "Hi", name: "Alena", post_id: 1, created_at: "2017-10-02 01:01:33", updated_at: "2017-10-02 01:01:33">]>

You can learn about other methods available on associations here: Ruby on Rails Guides: Association References

**Further Practice**

   * Try creating a full-fledged version of the veterinary office app that you've seen in the code challenges for this course. It should have an Owner model class that has_many instances of a Pet model class.
   * Try creating an automotive database app with Car and Truck model classes. Both cars and trucks should have a polymorphic has_many relationship with instances of a Part model class.

Further Reading

    Rails Guides: Nested Resources (http://guides.rubyonrails.org/routing.html#nested-resources)
    Rails Guides: Active Record Associations (http://guides.rubyonrails.org/association_basics.html)

## Student's Notes

> bin/rails c
   > post = Post.create(title: "Newest post")
   > Post.last.comments
   	=> #<ActiveRecord::Associations::CollectionProxy []>

   > Post.last.comments.empty?
   	=> true
   > Post.last.comments.present?
   	=> false

__app/views/posts/show.html.erb__
..
<div id="comments">
	<% if @post.comments.present? %>
		<h1>Comments</h1>
	<% end %>
	
	<%= render @post.comments %>
	<h2>Add a Comment</h2>
	<%= render partial: "comments/form", locals: {comment: @post.comments.new} %>
</div>
..

> bin/rails c
   > Post.first.comments.size

   >pp Post.first.comments.where(name: "Alena")
