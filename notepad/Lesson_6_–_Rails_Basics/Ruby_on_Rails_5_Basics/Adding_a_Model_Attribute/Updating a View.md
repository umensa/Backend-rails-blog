#Updating a View

**Challenge Task 1 of 1**

The app/views/pets/show.html.erb template outputs the pet's name attribute, but not its breed.
Add another <p> element to the template, with the value of @pet.breed embedded in it.
You'll need to use a <%= %> tag to embed the value.

___app/views/pets/show.html.erb___
<p>
  <strong>Name:</strong>
  <%= @pet.name %>
</p>

<!-- YOUR CODE HERE -->
	<p>
  	<strong>Name:</strong>
  	<%= @pet.breed %>
	</p>
