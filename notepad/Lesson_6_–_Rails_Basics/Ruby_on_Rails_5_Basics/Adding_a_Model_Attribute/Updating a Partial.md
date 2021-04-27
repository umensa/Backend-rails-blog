#Updating a Partial

**Challenge Task 1 of 1**

The "new" and "edit" forms for pets have a field for the name attribute, but not the breed attribute.
Update the `_form.html.erb` partial to add a text_field for the breed after the name field.

___app/views/pets/_form.html.erb___
<% form_for(pet) do |f| %>

  <div class="field">
    <%= f.label :name %>
    <%= f.text_field :name %>
  </div>

  <div class="field">
    YOUR CODE HERE
    <%= f.label :breed %>
    <%= f.text_field :breed %>
  </div>

  <div class="actions">
    <%= f.submit %>
  </div>
<% end %>

___app/views/pets/new.html.erb___
<h1>New Pet</h1>

<%= render 'form', pet: @pet %>

___app/views/pets/edit.html.erb___
<h1>Editing Pet</h1>

<%= render 'form', pet: @pet %>
