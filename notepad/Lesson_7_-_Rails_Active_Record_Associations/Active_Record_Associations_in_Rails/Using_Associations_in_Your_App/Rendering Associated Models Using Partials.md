# Rendering Associated Models Using Partials
You've got a working list of comments for each Post. Since each comment has only two attributes, this works okay. But once you start working with more complicated models, sticking their HTML code straight into their associated model's view may not work so well. We've used partials in previous courses to use the same HTML form code to both create and edit model objects. Let's try using partials here to render the HTML that shows a model.

## Teacher's Notes

Let's try using partials to render the HTML that shows a comment.

    Move comment HTML to partial template: app/views/comments/_comment.html.erb

<div>
  <strong><%= comment.name %> says:</strong>
  <%= comment.content %>
</div>

    Underscore in name indicates this is a partial.
    Note this code still expects a local variable named comment. We'll leave that and set it when we render the partial.

Back in views/posts/show.html.erb, we can call render with a partial: argument to render the partial:

  <% @post.comments.each do |comment| %>
    <%= render partial: "comments/comment", locals: {comment: comment} %>
  <% end %>

    render will look in the posts/ by default, so we need to add comments/ on front of partial name
    We leave underscore out of file name in partial: argument, .html.erb is added automatically
    locals: argument takes a hash with the names and values of local variables to set when rendering partial

There's a simpler way to do the same thing: we can loop through a collection and render a partial for each using render's collection: argument:

  <%= render partial: "comments/comment", collection: @post.comments, as: :comment %>

    as: argument takes symbol with name of local variable to assign

The collection: argument automatically assigns current member to local variable with same name as the partial, so we can remove as: :comment:

  <%= render partial: "comments/comment", collection: @post.comments %>

And here's the ultimate shortcut... we can pass just @post.comments to render.

  <%= render @post.comments %>

    render realizes you're passing it a collection, so it's as if you're passing it as the collection: argument.
    Also no need for a partial: argument. render sees Comment objects in the collection, so it looks in the views/comments folder for a partial named _comment.

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
	<!--
	<% @post.comments.each do |comment| %>		
		<div>
			<strong><%= comment.name %>says:</strong>
			<%= comment.content %>
		</div> -->
		<!-- <%= render partial: "comments/comment", locals: {comment: comment} %>
	<% end %>

	OR with collection argument
	<%= render partial: "comments/comment", collection: @post.comments,  as: :comment %>
	<%= render partial: "comments/comment", collection: @post.comments %> 
	-->
	<%= render @post.comments %>
</div>

<%= link_to 'Edit', edit_post_path(@post) %> |
<%= link_to 'Back', posts_path %>

__ app/views/comments/_comment.html.erb___
<div>
	<strong><%= comment.name %>says:</strong>
	<%= comment.content %>
</div>

# Rendering Collections

**Challenge Task 1 of 1**

As we set up in previous challenges, an Owner model has_many Pet instances. In the views/owners/show.html.erb template, an Owner object is available within the @owner instance variable. Using the template file and the views/pets/_ pet.html.erb partial, render a view that includes the name attribute for each Pet belonging to @owner.

__app/views/owners/show.html.erb__
 <h1>Owner: <%= @owner.name %></h1>
<div id="pets">
  <h2>Pets</h2>
  <!-- YOUR CODE HERE -->
  <%= render @owner.pets %>
</div>

__ app/views/pets/_pet.html.erb__
<div>
  <strong>Name:</strong>
  <%= <!--# YOUR CODE HERE --> pet.name %>
</div>
