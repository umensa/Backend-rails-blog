# Rendering Associated Models in Views
We can use all the same association methods we were using in the Rails console within controllers and views. That's going to be the key to allowing create, read, update, and delete actions on our associated models from a user's web browser. First, let's try applying that to viewing a list of the comments associated with a Post.

## Teacher's Notes



Back in our blog app, we can associate comments with a post in the Rails console. But users can't view a post's comments from their browser yet. Let's fix that.

We can use all the same association methods we were using in the Rails console within controllers and views. That's going to be the key to allowing create, read, update, and delete actions on our associated models from a user's web browser. First, let's try applying that to viewing a list of the comments associated with a Post.

Here's the most direct way:

<div id="comments">
  <h1>Comments</h1>
  <!-- The `comments` method returns an array-like collection, so we can call `each` on it: -->
  <% @post.comments.each do |comment| %>
    <div>
      <strong><%= comment.name %> says:</strong>
      <%= comment.content %>
    </div>
  <% end %>
</div>

Now you've got a working list of comments for each Post. This works okay for an associated model with only two attributes. But once you start working with more complex associated models, embedding their code in the view for a different model becomes unwieldy. Up next we'll look at a better way to break up your ERB code, using partials.

## Student's Notes

__app/views/posts/show.html.erb__
<p id="notice"><%= notice %></p>

<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Body:</strong>
  <%= @post.body %>
</p>

<div id="comments">
	<h1>Comments</h1>
	<% @post.comments.each do |comment| %>
		<div>
			<strong><%= comment.name %>says:</strong>
			<%= comment.content %>
		</div>
	<% end %>
</div>

<%= link_to 'Edit', edit_post_path(@post) %> |
<%= link_to 'Back', posts_path %>

___http://localhost:3000/posts/1___
