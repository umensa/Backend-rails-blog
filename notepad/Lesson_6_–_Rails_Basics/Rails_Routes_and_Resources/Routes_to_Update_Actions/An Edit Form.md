# An Edit Form
We have a controller action set up to load an existing Page model object for editing.
Now we just need to present a form to edit it with.

## Student's Notes

copy content of __app/views/pages/new.html.erb__ to 
__ app/views/pages/_form.html.erb__
<%= form_for(page) do |f| %> #form_for(without'@')
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

__app/views/pages/edit.html.erb__
<%= render 'form', page: @page %>

__app/views/pages/new.html.erb__
<%= render 'form', page: @page %>

# Moving the Pet Form to a Partial

**Challenge Task 1 of 5**

Move all the form code from the new.html.erb template to the _form.html.erb partial._

_app/views/pets/_form.html.erb_
<%= form_for(pet) do |f| %>
  <%= f.label :name %>
  <%= f.text_field :name %>
  <%= f.submit %>
<% end %>

**Challenge Task 2 of 5**

In new.html.erb, render the _form.html.erb partial._

___app/views/pets/new.html.erb___
<%= render 'form' %>

**Challenge Task 3 of 5**

In the call to render in new.html.erb, set up a pet local variable within the partial.
The value should be the object in @pet.

___app/views/pets/new.html.erb___
<%= render 'form', pet: @pet %>


**Challenge Task 4 of 5**

In the form partial, replace the reference to the @pet instance variable with a reference to the pet local variable.

_app/views/pets/_form.html.erb_
<%= form_for(pet) do |f| %>
  <%= f.label :name %>
  <%= f.text_field :name %>
  <%= f.submit %>
<% end %>

**Challenge Task 5 of 5**

Render the form partial from edit.html.erb as well. Set up the pet instance variable in the same way you did in new.html.erb.

___app/views/pets/edit.html.erb___
<%= render 'form', pet: @pet %>
