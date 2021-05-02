# Linking to Pages
Users can view a list of all our page titles, but they can't view the content of single Pages yet.
For our Posts resource, they can click a link on the list of all Posts to view an individual post.
Let's set up links to view single Pages as well.

## Teacher's Notes

The link_to method returns a string with the HTML for a link.

`<%= link_to("link text", "/link/path") %>`

More documentation is here.
(https://api.rubyonrails.org/classes/ActionView/Helpers/UrlHelper.html#method-i-link_to)

Let's say we need to set up links to view individual Page objects.
In the URL path, following /pages/, we need a string representing the ID of the Page object we want to load.
We'll set up the route like this:

`get '/pages/:id', to: 'pages#show'`

The colon followed by a name is a URL parameter.
A URL parameter captures part of the request path, and makes it available within the controller in the params hash.
So if we type :id here, it will be available later as params[:id].
We can name the parameter whatever we want, but by convention the name :id is used for model record IDs.

## Student's Notes

__app/views/pages/index.html.erb__
<%  @pages.each do |page| %>
	<p><%= link_to "link text", "/link/path" %></p>
<% end %>

__config/routes.rb__
Rails.application.routes.draw do
  resources :posts
  get '/pages', to: 'pages#index'
  get '/pages/:id', to: 'pages#show'
end

# Linking to Model Objects

**Challenge Task 1 of 1**

Embed a link in this template's output using the link_to method.
The link text should say "List of all Pets", and the link path should be "/pets".

___app/views/main.html.erb___
<p><%= link_to "List of all Pets", "/pets" %></p>

# Set Up a URL Parameter

**Challenge Task 1 of 1**

Set up a route to view an individual Pet.
It should match GET requests with a path of /pets/ followed by the ID of the particular Pet: /pets/3, /pets/27, etc. You'll need to set it up so that the ID from the path is available within the controller as params[:id]. Matching requests should be routed to the show action method on PetsController.

___routes.rb___
Rails.application.routes.draw do
  # YOUR CODE HERE
  get '/pets/:id', to: 'pets#show'
end
