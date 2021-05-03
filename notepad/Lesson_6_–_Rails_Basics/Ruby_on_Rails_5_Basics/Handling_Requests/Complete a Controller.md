#Complete a Controller

**Challenge Task 1 of 1**

The app/views/pets/index.html.erb template will get rendered automatically by the index action method on the PetsController.
But it needs the @pets instance variable to be set to the list of all Pet objects from the database.
Within the index method, call the Pet.all method, and assign the result to the @pets instance variable.

___app/controllers/pets_controller.rb___

 class PetsController < ApplicationController

  def index
    # YOUR CODE HERE
    @pet = Pet.all
  end

end

___app/views/pets/index.html.erb___
<p id="notice"><%= notice %></p>

<h1>Pets</h1>

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Birthdate</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <% @pets.each do |pet| %>
      <tr>
        <td><%= pet.name %></td>
        <td><%= pet.birthdate %></td>
      </tr>
    <% end %>
  </tbody>
</table>

<br>
