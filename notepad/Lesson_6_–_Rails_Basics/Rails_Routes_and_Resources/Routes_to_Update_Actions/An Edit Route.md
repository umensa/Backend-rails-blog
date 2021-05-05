# An Edit Route
Now our users can create a new Page.
But they'd better get it right the first time, because right now they can't go back and change what they've entered...
Maybe we should fix that.
Let's give them a form to allow them to update existing Pages.

## Teacher's Notes

When a user wants to create a new model object, the browser sends an HTTP GET request to retrieve a blank form.
When they submit the new form, the browser sends an HTTP POST request to create a new record on the server.

And when a user wants to edit an existing model object, the browser needs to send an HTTP GET request to retrieve that form as well.
The difference is that the edit form will be pre-populated with the existing object's data.

Another difference is that when you're modifying existing data on the server (rather than adding new data), you're supposed to use a PUT or PATCH request rather than a POST request.
So when you click the submit button on the edit form, that's what your browser sends to the server: a PATCH request.

## Student's Notes

__config/routes.rb__
Rails.application.routes.draw do
  resources :posts
  ...
  get '/pages/:id/edit', to: 'pages#edit', as: 'edit_page'
end

__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  ...

  def edit
    @page = Page.find(params[:id])
  end
end

__app/views/pages/edit.html.erb__
form to edit <%= @page.title %> Page will go here.

__app/views/pages/show.html.erb__
...

<%= link_to 'Edit', edit_page_path(@page) %>

# An Edit Route

**Challenge Task 1 of 1**

Add a route to edit an existing Pet.
It should match GET requests with a path of /pets/, the ID of the particular Pet, and the suffix /edit: /pets/3/edit, /pets/27/edit, etc.
You'll need to set it up so that the ID from the path is available within the controller as params[:id].
Matching requests should be routed to the edit action method on PetsController.

___routes.rb___
Rails.application.routes.draw do
  get '/pets/new', to: 'pets#new'
  get '/pets/:id', to: 'pets#show'
  post '/pets', to: 'pets#create'
  get '/pets/:id/edit', to: 'pets#edit'
end
