# Deleting Pages
Our users can create Pages, read Pages, update Pages... 
what's left? 
Oh, right, deleting Pages!
For every resource you create, there may come a time when you don't want it any more.
So, let's allow our users to delete Pages.

## Teacher's Notes

Deleting model records usually first requires providing a link that sends a DELETE request:

`<%= link_to 'Delete', @page, method: :delete %>`

You'll also need a route that sends the DELETE requests to the appropriate controller action:

`delete '/pages/:id', to: 'pages#destroy'`

The controller action usually performs the following operations:

  def destroy
    # Look up the model record to destroy
    # based on the ID from the request path.
    @page = Page.find(params[:id])
    # Delete the matching record.
    @page.destroy
    # Redirect the browser to another
    # appropriate page.
    redirect_to pages_path
  end

## Student's Notes

__config/routes.rb__
Rails.application.routes.draw do
  resources :posts
  ...
  patch '/pages/:id', to: 'pages#update'
  delete '/pages/:id', to: 'pages#destroy'
end

__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  ...

  def destroy
    @page = Page.find(params[:id])
    @page.destroy
    redirect_to pages_path
  end

  private

    def page_params
      params.require(:page).permit(:title, :body, :slug)
    end
end

__app/views/pages/show.html.erb__
...

<%= link_to 'Edit', edit_page_path(@page) %>
<%= link_to 'Delete', @page, method: :delete %>

# A Delete Action 

**Challenge Task 1 of 3**

We've set up the following in routes.rb:

`get '/pets', to: 'pets#index', as: 'pets'
delete '/pets/:id', to: 'pets#delete'`

Within the delete method on PetsController, use the :id parameter to find the matching Pet record, and assign the result to the @pet instance variable.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def index
    @pets = Pet.all
  end

  # ...

  def delete

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])
  end
end

**Challenge Task 2 of 3**

Destroy the Pet object that you looked up via Pet.find.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def index
    @pets = Pet.all
  end

  # ...

  def delete

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])
    @pet.destroy
  end
end

**Challenge Task 3 of 3**

Finally, use the redirect_to method to redirect the browser to the path with the list of all Pets.
Remember, this is how it's set up in routes.rb:

`get '/pets', to: 'pets#index', as: 'pets'`

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def index
    @pets = Pet.all
  end

  # ...

  def delete

    # YOUR CODE HERE
    @pet = Pet.find(params[:id])
    @pet.destroy
    redirect_to pets_path
  end
end
