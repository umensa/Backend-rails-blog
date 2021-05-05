# Nested Routes and Resources
So far we've just relied on the show view for Posts to show a list of comments. That relies on an existing route for Posts. But to create, update, or delete comments, we're going to need a new set of routes, one that indicates which Post the Comment belongs to.

## Teacher's Notes

So far we've just relied on the show view for Posts to show a list of comments. That relies on an existing route for Posts. But to create, update, or delete comments, we're going to need a new set of routes, one that indicates which Post the Comment belongs to.

    If we were adding comments as a standalone model, we'd add a set of routes like these to config/routes.rb:

  get    '/comments',          to: 'comments#index', as: 'comments'
  post   '/comments',          to: 'comments#create'
  get    '/comments/new',      to: 'comments#new',   as: 'new_comment'
  get    '/comments/:id',      to: 'comments#show',  as: 'comment'
  get    '/comments/:id/edit', to: 'comments#edit',  as: 'edit_comment'
  patch  '/comments/:id',      to: 'comments#update'
  delete '/comments/:id',      to: 'comments#destroy'

    But each comment belongs to a post.
    When we ask to view a list of comments, we need to know which post we're getting comments for. So let's add a :post_id URL parameter in the route path, ahead of /comments.
    By the way, the URL parameter is named :post_id to distinguish it from the Comment ID, which is named just :id.
    So that it's clear that the start of the path is a Post ID, we'll add /posts to the start of the path also.
    When we take a form submission to create a new comment, we'll need to know what post we're creating a comment for. So we'll add /posts/:post_id at the start of that path, too.
    Basically, for every CRUD operation on comments, we're going to need to know what Post we're working with as well. So let'd copy /posts/:post_id and paste it in front of every route path for comments.

  get    '/posts/:post_id/comments',          to: 'comments#index', as: 'comments'
  post   '/posts/:post_id/comments',          to: 'comments#create'
  get    '/posts/:post_id/comments/new',      to: 'comments#new',   as: 'new_comment'
  get    '/posts/:post_id/comments/:id',      to: 'comments#show',  as: 'comment'
  get    '/posts/:post_id/comments/:id/edit', to: 'comments#edit',  as: 'edit_comment'
  patch  '/posts/:post_id/comments/:id',      to: 'comments#update'
  delete '/posts/:post_id/comments/:id',      to: 'comments#destroy'

    These route names will give us path helper methods like comments_path, new_comment_path, etc.
    But the paths also need a Post ID now, so we'll need to provide a Post each time we call a helper method.
    Let's update the route names to reflect this. We'll add the word post_ before comment in each.

  get    '/posts/:post_id/comments',          to: 'comments#index', as: 'post_comments'
  post   '/posts/:post_id/comments',          to: 'comments#create'
  get    '/posts/:post_id/comments/new',      to: 'comments#new',   as: 'new_post_comment'
  get    '/posts/:post_id/comments/:id',      to: 'comments#show',  as: 'post_comment'
  get    '/posts/:post_id/comments/:id/edit', to: 'comments#edit',  as: 'edit_post_comment'
  patch  '/posts/:post_id/comments/:id',      to: 'comments#update'
  delete '/posts/:post_id/comments/:id',      to: 'comments#destroy'

    With those changes made, bin/rails routes outputs:

           Prefix Verb   URI Pattern                                 Controller#Action
    post_comments GET    /posts/:post_id/comments(.:format)          comments#index
                  POST   /posts/:post_id/comments(.:format)          comments#create
 new_post_comment GET    /posts/:post_id/comments/new(.:format)      comments#new
     post_comment GET    /posts/:post_id/comments/:id(.:format)      comments#show
edit_post_comment GET    /posts/:post_id/comments/:id/edit(.:format) comments#edit
                  PATCH  /posts/:post_id/comments/:id(.:format)      comments#update
                  DELETE /posts/:post_id/comments/:id(.:format)      comments#destroy

    Putting /posts/:post_id in each path and post_ in each route name is a lot of repetition.
    Instead, we can nest the routes under the :posts resource.
    Nesting routes under a resource will add an ID parameter for that resource to the start of each nested route's path.
    So nesting under the :posts resource will automatically add /posts/:post_id to the start of each comment route. We can remove /posts/:post_id from the start of each nested path.
    Nesting under a resource will also add its name to the start of each nested resource name. So we can remove post_ from each route name.

  resources :posts do
    get    '/comments',          to: 'comments#index', as: 'comments'
    post   '/comments',          to: 'comments#create'
    get    '/comments/new',      to: 'comments#new',   as: 'new_comment'
    get    '/comments/:id',      to: 'comments#show',  as: 'comment'
    get    '/comments/:id/edit', to: 'comments#edit',  as: 'edit_comment'
    patch  '/comments/:id',      to: 'comments#update'
    delete '/comments/:id',      to: 'comments#destroy'
  end

    Just as we replaced 7 Post routes with resources :posts in an earlier course, we can replace these 7 Comment routes with resources :comments.

  resources :posts do
    resources :comments
  end

    Because resources :comments is nested within the :posts resource, every Comment route path still has /posts/:post_id at the start.
    And every Comment route name includes post_

## Student's Notes

__config/routes.rb__
Rails.application.routes.draw do
  resources :posts do
    resources :comments
  end
  resources :pages
end

# Nested Routes and Resources

**Challenge Task 1 of 1**

Every Pet belongs to an Owner, so we want an owner_id parameter as part of the URL for all of our Pet routes:

Verb   URI Pattern                               Controller#Action
GET    /owners/:owner_id/pets(.:format)          pets#index
POST   /owners/:owner_id/pets(.:format)          pets#create
GET    /owners/:owner_id/pets/new(.:format)      pets#new
GET    /owners/:owner_id/pets/:id/edit(.:format) pets#edit
GET    /owners/:owner_id/pets/:id(.:format)      pets#show
PUT    /owners/:owner_id/pets/:id(.:format)      pets#update
DELETE /owners/:owner_id/pets/:id(.:format)      pets#destroy

Make the necessary changes here in config/routes.rb to set all of the above routes up. (You can set up routes for owners as well if you want, but we'll only be checking whether the above routes exist.)

__config/routes.rb__
Rails.application.routes.draw do

  # YOUR CODE HERE
  resources :owners do
    resources :pets
  end

end
