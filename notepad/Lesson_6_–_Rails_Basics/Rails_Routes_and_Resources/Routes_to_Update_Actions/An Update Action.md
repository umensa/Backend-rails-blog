# An Update Action
We've successfully created a form for editing an existing Page, and populated it with the Page's attributes.
But if we submit the form, we see that a so-called HTTP PATCH request is being sent by the browser, and there's no route for that type of request.
So to process these requests, we'll need to go into routes.rb add a PATCH route.

## Teacher's Notes

A controller action to update an existing model object usually performs these operations:

  def update
    # Look up the existing model record based
    # on an ID from the request path.
    @page = Page.find(params[:id])
    # Filter the form parameters to ensure no
    # malicious parameters were added.
    page_params = params.require(:page).permit(:title, :body, :slug)
    # Use the filtered parameters to update
    # the existing model record.
    @page.update(page_parameters)
    # Redirect the browser to another location
    # so that it doesn't just sit there displaying
    # the submitted form.
    redirect_to @page
  end

## Student's Notes

__config/routes.rb__
Rails.application.routes.draw do
  resources :posts
  ...
  patch '/pages/:id', to: 'pages#update'
end

__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  def index
    @pages = Page.all
  end

  def show
    @page = Page.find(params[:id])
  end

  def new
    @page = Page.new
  end

  def create
    @page = Page.new(page_params)
    @page.save
    redirect_to @page
  end

  def edit
    @page = Page.find(params[:id])
  end

  def update
    @page = Page.find(params[:id])
    @page.update(page_params)
    redirect_to @page
  end

  private

    def page_params
      params.require(:page).permit(:title, :body, :slug)
    end
end

# An Update Action

**Challenge Task 1 of 5**

We've set up the following in routes.rb:

`patch '/pets/:id', to: 'pets#update'`

Within the update method on PetsController, use the :id parameter to find the matching Pet record, and assign the result to the @pet instance variable.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def edit
    @pet = Pet.find(params[:id])
  end

  def update

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])

  end
end

**Challenge Task 2 of 5**

We've got parameters like this coming in from a PATCH request:

{
  ...,
  "pet"=>{"name"=>"Snowflake"},
  "commit"=>"Update Pet",
  "id"=>"3",
  ...
}

We need to set the controller's update method up to accept these parameters.
Start by using the require method to require that the pet parameter group be present.
(You may want to assign the result value to a variable, as we'll be using that value in later steps of this challenge.)

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def edit
    @pet = Pet.find(params[:id])
  end

  def update

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])
    pet_params = params.require(:pet).permit(:name, :commit)
    @pet.update(pet_params)

  end
end

**Challenge Task 3 of 5**

Here's the full set of parameters coming in from a PATCH request again:

{
  ...,
  "pet"=>{"name"=>"Snowflake"},
  "commit"=>"Update Pet",
  "id"=>"3",
  ...
}

Now, take the pet parameter group returned from require, and use the permit method on it to allow the name parameter.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def edit
    @pet = Pet.find(params[:id])
  end

  def update

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])
    pet_params = params.require(:pet).permit(:name)
  end
end

**Challenge Task 4 of 5**

Update the Pet object with the list of parameters returned from permit.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def edit
    @pet = Pet.find(params[:id])
  end

  def update

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])
    pet_params = params.require(:pet).permit(:name)
    @pet.update(pet_params)

  end
end

**Challenge Task 5 of 5**

Finally, pass the updated Pet object to redirect_to, to redirect the browser to the show view.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def edit
    @pet = Pet.find(params[:id])
  end

  def update

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])
    pet_params = params.require(:pet).permit(:name)
    @pet.update(pet_params)
    redirect_to @pet
  end
end
