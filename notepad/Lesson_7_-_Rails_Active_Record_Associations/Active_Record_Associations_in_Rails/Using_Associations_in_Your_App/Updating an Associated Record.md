# Updating an Associated Record
We've added a way to create comments that belong to a post. Now let's add a means of updating those comments.

## Teacher's Notes

We've added a way to create comments that belong to a post. Now let's add a means of updating those comments.

    We want an "edit" link to appear next to each comment.
    We'll get that by editing the _comment partial.

views/comments/_ comment.html.erb

<div class="comment-admin">
  <%= link_to "Edit", edit_post_comment_path(@post, comment) %>
</div>

    Next we need an edit action on the CommentsController:

controllers/comments_controller.rb

  def edit
    @post = Post.find(params[:post_id])
    @comment = Comment.find(params[:id])
  end

    @post = Post.find(params[:post_id]) code is repeated between create and edit actions, and we'll need @post for other actions
    Use before_action to set @post

class CommentsController < ApplicationController
  before_action :set_post
  def create
    @comment = @post.comments.create(comment_params)
    redirect_to @post
  end
  def edit
    @comment = Comment.find(params[:id])
  end
  private
  def comment_params
    params.require(:comment).permit(:name, :content)
  end
  def set_post
    @post = Post.find(params[:post_id])
  end
end

    When we click the "Edit" link, it calls our edit action, but there's no view. So let's create one:

views/comments/edit.html.erb

<h1>Edit Comment</h1>
<%= render partial: "form", locals: {comment: @comment} %>

    We need an update action on CommentsController so we can submit the form:

  def update
    @comment = Comment.find(params[:id])
    @comment.update(comment_params)
    redirect_to @post # @post will be set by before_action
  end

## Student' Notes

__app/views/comments/_ comment.html.erb__
<div>
	<strong><%= comment.name %> says:</strong>
	<%= comment.content %>
	<div class="comment-admin">
		<%= link_to "Edit", edit_post_comment_path(@post, comment) %>
	</div>
</div>

__app/controllers/comments_controller.rb__
class CommentsController < ApplicationController
  before_action :set_post

  def create
    @comment = @post.comments.create(comment_params)
    redirect_to @post
  end

  def edit
    @comment = Comment.find(params[:id])
  end

  def update
    @comment = Comment.find(params[:id])
    @comment.update(comment_params)
    redirect_to @post
  end

  private
  def comment_params
    params.require(:comment).permit(:name, :content)
  end

  def set_post
    @post = Post.find(params[:post_id])
  end
end

__app/views/comments/edit.html.erb__
<h1>Edit Comment</h1>
<%= render partial: "form", locals: {comment: @comment} %>
