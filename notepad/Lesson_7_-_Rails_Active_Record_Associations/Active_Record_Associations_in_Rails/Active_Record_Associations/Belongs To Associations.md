# Belongs To Associations
We can easily look up the Comments that belong to a Post. But the way things are set up now, we might have a little more trouble looking up the Post that a Comment belongs to. The belongs_to association can fix that.

## Teacher's Notes

We can easily look up the Comments that belong to a Post. But the way things are set up now, we might have a little more trouble looking up the Post that a Comment belongs to.

    Suppose all we had was a comment, and we wanted to get the Post that it belongs to.
        Go to app/models/comment.rb, and add: belongs_to :post.
        Now we can load up a Comment: comment = Comment.last, and access the Post it belongs to by calling its new post method: comment.post. We already made all the database changes we needed when adding the has_many :comments association to the Post class, so our belongs_to :post association works immediately.

Now you know how to set up belongs_to associations. Anytime you set up a has_many association from your first model to a second model, you're going to want to set up a belongs_to association from the second model back to the first.


## Student's Notes

> comment = Comment.last
> Post.find(comment.post_id)
	The same > Post.last.comments

__app/models/comments.rb__
class Comment < ApplicationRecord
  belongs_to :post
end

> comment = Comment.last
> comment.post

# "Belongs To" Associations

**Challenge Task 1 of 1**

The Owner model has_many Pet instances, but there's no way to access an Owner from its Pet. In the Pet model class, specify that every pet belongs to an owner.

Important: In each task of this code challenge, the code you write should be added to the code from the previous task.

__models/pet.rb__
class Pet < ApplicationRecord
	belongs_to :owner
end
