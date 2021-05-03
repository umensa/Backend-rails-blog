# Route for New Pages
Our users can view a list of all Pages.
They can click a link to view an individual Page.
What they CAN'T do right now is create new pages; we had to go into the Rails console to do that.
Our next task is to set up a form so that it's easy for our USERS to create Pages, too.

## Teacher's Notes

HTTP GET requests are intended for getting data from the server.
HTML forms are just another type of data.
So when a user wants to create a new Page, the browser should send an HTTP GET request to retrieve a blank HTML form.

When you're adding new data, though, you're supposed to use an HTTP POST request instead.
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
  get '/pages/new', to: 'pages#new'
  get '/pages/:id', to: 'pages#show', as: 'page'

  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end

# Route for New Pets

**Challenge Task 1 of 1**

Add a route that sends all GET requests for the /pets/new path to the PetsController's new action method.

___routes.rb___
Rails.application.routes.draw do
  get '/pets/new', to: 'pets#new'
  get '/pets/:id', to: 'pets#show'
end
