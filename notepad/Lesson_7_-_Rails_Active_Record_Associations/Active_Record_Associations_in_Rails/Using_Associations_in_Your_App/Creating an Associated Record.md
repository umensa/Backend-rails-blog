# Creating an Associated Record
So far we've only been able to create Comments via the Rails console. It's finally time to set up creation of Comments via the browser.

## Teacher's Notes

So far we've only been able to create Comments via the Rails console. It's finally time to set up creation of Comments via the browser.

This is going to work a lot like the creation of standalone models like Posts and Pages that we saw in previous courses. The difference is that each Comment will be created in the context of the Post it belongs to. The form to add a Comment will be on a Post's show page. And we'll need a Post ID to use when saving the Comment model object to the database.

views/posts/show.html.erb

<div id="comments">
  <h1>Comments</h1>
  <%= render @post.comments %>
  <!-- NEW CODE BELOW: -->
  <h2>Add a Comment</h2>
  <%= render partial: "comments/form", locals: {comment: @post.comments.new} %>
</div>

views/comments/_ form.html.erb

<%= form_for [@post, comment] do |f| %>
  <div class="field">
    <%= f.label :name %>
    <%= f.text_field :name %>
  </div>

  <div class="field">
    <%= f.label :content, "Comment" %>
    <%= f.text_area :content %>
  </div>

  <div class="actions">
    <%= f.submit %>
  </div>
<% end %>

    Next we need a CommentsController: bin/rails generate controller Comments

controllers/comments_controller.rb

class CommentsController < ApplicationController
  # No `new` action because form is provided by PostsController#show
  def create
    @post = Post.find(params[:post_id])
    # Create associated model, just like we did in the console before
    @comment = @post.comments.create(comment_params)
    # We want to show the comment in the context of the Post
    redirect_to @post
  end
  private
  def comment_params
    params.require(:comment).permit(:name, :content)
  end
end

## Student's Notes

__app/views/posts/show.html.erb__
..
<div id="comments">
	<h1>Comments</h1>
	<%= render @post.comments %>
	<h2>Add a Comment</h2>
	<%= render partial: "comments/form", locals: {comment: @post.comments.new} %>
</div>
..

__app/views/comments/_ form.html.erb__
<%= form_for [@post, comment] do |f| %>
	<div class="field">
		<%= f.label :name %>
		<%= f.text_field :name %>
	</div>

	<div class="field">
		<%= f.label :content, "Comment" %>
		<%= f.text_area :content %>
	</div>

	<div class="actions">
		<%= f.submit %>
	</div>
<% end %>

> bin/rails g controller Comments

__app/controllers/comments_controller.rb__
class CommentsController < ApplicationController
  def create
    @post = Post.find(params[:post_id])
    @comment = @post.comments.create(comment_params)
    redirect_to @post
  end

  private
  def comment_params
    params.require(:comment).permit(:name, :content)
  end
end
