# Path Helpers
Before we fix the controller issue, we need to take a quick detour and show you a better way to create links within your own app.
Having to type "/pages/#{page.id}" everywhere you want to link to an individual page is tedious and error-prone.
If we want, we can name the route.
This will have Rails create a path helper method for us that will return that same path string.

## Teacher's Notes

Having to type "/pages/#{page.id}" everywhere you want to link to an individual page is tedious and error-prone.
If we want, we can name the route.
This will have Rails create a path helper method for us that will return that same path string.

In routes.rb, add an as: argument at the next of the route, with a string value.
That string will be used as the route name.
It can be anything we want, but since this is a route to get a single Page, a name of 'page' would be conventional.

___config/routes.rb___
`get '/pages/:id', to: 'pages#show', as: 'page'`

___app/views/index.html.erb___
Now, in your templates, you can replace "/pages/#{page.id}" with page_path(page).

It will look at the ID of the model object you pass in, and return a string with a path that includes that ID.

## Student's Notes

___app/views/index.html.erb___
<%  @pages.each do |page| %>
	<p><%= link_to page.title, page %></p>
<% end %>

# Path Helpers

**Challenge Task 1 of 1**

Let's add a pets_path helper method. Assign a name of 'pets' to the get '/pets' route.

___routes.rb___
Rails.application.routes.draw do
  get '/pets', to: 'pets#index', as: 'pets'
end
