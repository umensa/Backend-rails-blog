# Deleting an Associated Record
Our blog app now lets us create, read, and update Comments that belong to a Post. Lastly, we need to support deleting Comments.

## Teacher's Notes

Our blog app now lets us create, read, and update Comments that belong to a Post. Lastly, we need to support deleting Comments.

    We can set up a delete link in the _comment.html.erb partial:

views/comments/_ comment.html.erb

<div class="comment-admin">
  <%= link_to "Edit", edit_post_comment_path(@post, comment) %>
  <!-- NEW CODE BELOW -->
  <%= link_to "Delete", [@post, comment], method: :delete %>
</div>

    We need a destroy action on the CommentsController:

  def destroy
    @comment = Comment.find(params[:id])
    @comment.destroy
    redirect_to @post
  end

Further Reading

Rails Guides: Nested Resources
(http://guides.rubyonrails.org/routing.html#nested-resources)

Extra Credit

We currently have a before_action named set_post on the CommentsController. Try adding a second before_action named set_comment that sets the @comment instance variable.

## Student's Notes

__app/views/comments/_ comment.html.erb__
<div>
	<strong><%= comment.name %> says:</strong>
	<%= comment.content %>
	<div class="comment-admin">
		<%= link_to "Edit", edit_post_comment_path(@post, comment) %>
		<%= link_to "Delete", [@post, comment], method: :delete %>
	</div>
</div>

__app/controllers/comments_controller.rb__
..
def destroy
    @comment = Comment.find(params[:id])
    @comment.destroy
    redirect_to @post
  end
..
