# Finding a Page
We're trying to show individual Page records, and we've set up a route to the "show" method on the "PagesController".
But that method doesn't exist yet.
Let's visit the PagesController code, and add a show method now.

## Teacher's Notes

This video recommends calling render text:, which works fine in Rails 5.0 (the recommended version to use when following along with this course).
But if you happen to have generated your app using Rails 5.1 or later, render text: no longer works.

In both Rails 5.0 and 5.1, you can replace render text: with render plain:, and it will work correctly.

## Student's Notes

__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  def index
    @pages = Page.all
  end

  def show
    @page = Page.find(params[:id])
    render text: @page.title
  end
end

# Finding a Model Object

**Challenge Task 1 of 1**

We've set up the following in routes.rb:

get '/pets/:id', to: 'pets#show'

But that controller action method doesn't exist yet.
Create it now.
Within the method, use the :id parameter to find the matching Pet record, and assign the result to the @pet instance variable.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController

  # YOUR CODE HERE
  def show
    @pet = Pet.find(params[:id])
  end

end
