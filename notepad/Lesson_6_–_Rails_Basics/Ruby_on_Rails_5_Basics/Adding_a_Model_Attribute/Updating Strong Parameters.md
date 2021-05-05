#Updating Strong Parameters
Rails is mistakenly trying to "protect" you from malicious parameters.
We need to fix that.

##Teacher's Notes
You can read more about _Rails Strong Parameters here_.
(https://edgeguides.rubyonrails.org/action_controller_overview.html#strong-parameters)

**Challenge Task 1 of 1**

The `_form.html.erb` partial has been updated with a "breed" field.
But we're seeing an "Unpermitted parameter: breed" message in the Rails log.
Add :breed as a permitted parameter in the controller.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController

  def new
    @pet = Pet.new
  end

  def create
    @pet = Pet.new(pet_params)
    @pet.save
    redirect_to pets_url
  end

  private

    def pet_params
      params.require(:pet).permit(:name, :birthdate, :breed)
    end

end

___app/views/pets/_form.html.erb___
<%= form_for(pet) do |f| %>

  <div class="field">
    <%= f.label :name %>
    <%= f.text_field :name %>
  </div>

  <div class="field">
    <%= f.label :birthdate %>
    <%= f.date_select :birthdate %>
  </div>

  <div class="field">
    <%= f.label :breed %>
    <%= f.text_field :breed %>
  </div>

  <div class="actions">
    <%= f.submit %>
  </div>
<% end %>
