# Route to Create Pages
When we submit our form for a new Page, we see the error "No route matches [POST] '/pages'".
Notice that it's not saying [GET] '/pages', it's saying POST.
We only have GET request routes for pages right now, though.
We'll need to add a POST route.

## Teacher's Notes

When you're adding new data to the server, your browser sends an HTTP POST request.
So, when you click the submit button on an HTML form, that's what your browser sends to the server: a POST request with the form contents.

For this reason, setting up a form to add new instances of a resource usually requires two routes in your routes.rb file.

Suppose we were setting up a form for new Page records.
We'd first need a route to GET the HTML form:

`get '/pages/new', to: 'pages#new'`

Then we'd need a second route to accept the POST request when the form is submitted:

`post '/pages', to: 'pages#create'`

## Student's Notes

__config/routes.rb__
Rails.application.routes.draw do
  resources :posts
  get '/pages', to: 'pages#index'
  post '/pages', to: 'pages#create'
  get '/pages/new', to: 'pages#new', as: 'new_page'
  get '/pages/:id', to: 'pages#show', as: 'page'

  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end

# Route to Create Pets

**Challenge Task 1 of 1**

Add a route that sends all POST requests for the `/pets` path to the PetsController's `create` action method.

___routes.rb___
Rails.application.routes.draw do
  get '/pets/new', to: 'pets#new'
>  post '/pets', to: 'pets#create'
  get '/pets/:id', to: 'pets#show'
end
