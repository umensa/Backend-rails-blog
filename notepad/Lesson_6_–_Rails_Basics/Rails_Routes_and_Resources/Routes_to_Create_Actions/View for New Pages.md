# View for New Pages
We have the /pages/new path routed to the PagesController's new method.
In that method, we've set up a new Page object in the @page instance variable.
Now, we need to set up an ERB view template that creates a form based on that Page object.

## Teacher's Notes

The form_for method takes a model object, and generates an HTML form for it.
`
# This will embed the form HTML in the output.
# Here, a form will be generated for the object
# in @page.
<%= form_for(@page) do |f| %>
  <div class="field">
    # This will output a label for the "title" field.
    <%= f.label :title %>
    # This will output a text field used to set the
    # title attribute of the Page object.
    <%= f.text_field :title %>
  </div>
``
  <div class="field">
    # This will output a label for the "body" field.
    <%= f.label :body %>
    # This will output a larger text field used to set the
    # body attribute of the Page object.
    <%= f.text_area :body %>
  </div>
``
  <div>
    # Outputs a button used to submit the form.
    <%= f.submit %>
  </div>
<% end %>
`
You can read more about form_for in the official Rails documentation.
(https://guides.rubyonrails.org/form_helpers.html#binding-a-form-to-an-object)

Want to learn more about HTML forms? Check out our course on the topic.

## Student's Notes

__app/views/pages/new.html.erb__
<%= form_for(@page) do |f| %>
	<div class="field">
		<%= f.label :title %>
		<%= f.text_field :title %>
	</div>

	<div class="field">
		<%= f.label :body %>
		<%= f.text_area :body %>
	</div>

	<div class="field">
		<%= f.label :slug %>
		<%= f.text_field :slug %>
	</div>

	<div>
		<%= f.submit %>
	</div>
<% end %>

__config/routes.rb__
Rails.application.routes.draw do
  resources :posts
  get '/pages', to: 'pages#index'
  get '/pages/new', to: 'pages#new', `as: 'new_page'`
  get '/pages/:id', to: 'pages#show', as: 'page'

  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end

__app/views/pages/index.html.erb__
<h1>Blog Pages</h1>

<%  @pages.each do |page| %>
	<p><%= link_to page.title, page %></p>
<% end %>

`<%= link_to 'New Page', new_page_path %>`

# Controller Action for New Pets

**Challenge Task 1 of 1**

We need a new controller action that renders a form for a new Pet.
Set up a method named new that stores a new Pet object with blank attributes in the @pet instance variable, for rendering in the view's form.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController

  # YOUR CODE HERE
  def new
  	@pet = Pet.new
  end

end

# View for New Pets

**Challenge Task 1 of 4**

The new action method on the PetsController includes the following code:

def new
  @pet = Pet.new
end

In the template, use the form_for method within an output ERB tag to set up an HTML form based on this empty object. Don't forget to provide a block to form_for. The block should take a single parameter that holds the HTML form object. Also remember that you need a separate ERB tag to end the block.

___app/views/pets/new.html.erb___
<%= form_for(@pet) do |f| %>

​<% end %>

**Challenge Task 2 of 4**

Within the form_for block, output a label for the name field. (Don't worry about enclosing it in a <div> or any other formatting.)

___app/views/pets/new.html.erb___
<%= form_for(@pet) do |f| %>
	<div class="field">
		<%= f.label :name %>
	</div>
<% end %>

**Challenge Task 3 of 4**

Within the form_for block, output a text field for the name attribute.

___app/views/pets/new.html.erb___
<%= form_for(@pet) do |f| %>
	<div class="field">
		<%= f.label :name %>
		<%= f.text_field :name %>
	</div>
<% end %>

**Challenge Task 4 of 4**

Within the form_for block, output a submit button.

___app/views/pets/new.html.erb___
<%= form_for(@pet) do |f| %>
	<div class="field">
		<%= f.label :name %>
		<%= f.text_field :name %>
	</div>
	<div>
		<%= f.submit %>
	</div>
<% end %>
