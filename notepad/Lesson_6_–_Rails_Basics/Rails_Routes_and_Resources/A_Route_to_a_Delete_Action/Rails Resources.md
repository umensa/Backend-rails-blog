# Rails Resources
We have routes leading to seven action methods on our controller...
It took us seven lines of code in our routes.rb file to set all these routes up.
But because these are the seven conventional routes for any given Rails resource, and you're going to need to set up these same seven routes for most resources you create, there's a shortcut you can use instead.

## Teacher's Notes

These are the seven conventional routes that almost any Rails resource will have:
`
Rails.application.routes.draw do
  get    '/pages',          to: 'pages#index'
  post   '/pages',          to: 'pages#create'
  get    '/pages/new',      to: 'pages#new',  as: 'new_page'
  get    '/pages/:id',      to: 'pages#show', as: 'page'
  get    '/pages/:id/edit', to: 'pages#edit', as: 'edit_page'
  patch  '/pages/:id',      to: 'pages#update'
  delete '/pages/:id',      to: 'pages#destroy'
end
`
You can replace all of the above with a single line:
`
Rails.application.routes.draw do
  resources :pages
end
`

`resources :pages` will create all the same routes (named in the same way) as the preceding seven lines of code.

Have questions about this video? Start a discussion with the community and Treehouse staff.

## Student's Notes

__config/routes__
Rails.application.routes.draw do
  resources :posts
  resources :pages
end

# A Pets Resource

**Challenge Task 1 of 1**

Replace all the following routes with a single line.

Important: In each task of this code challenge, the code you write should be added to the code from the previous task.

___routes.rb___
Rails.application.routes.draw do
	resources :pets
end
