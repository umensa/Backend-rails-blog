# Controller Action to Create Pages
We've set up a route so that form submissions get sent to the PagesController's create method.
But that method doesn't exist yet.
Let's set it up now.
Within the create method, we're going to need to specify which parameters are safe to use to create the new Page object.

## Teacher's Notes

**Important Update**

This video recommends calling `render text:`, which works fine in Rails 5.0 (the recommended version to use when following along with this course).
But if you happen to have generated your app using Rails 5.1 or later, render text: no longer works.

In both Rails 5.0 and 5.1, you can replace `render text:` with `render plain:`, and it will work correctly.

**Strong Parameters**

Suppose you have a parameters object with a bunch of parameters you don't want.
All the parameters you do want are nested under the page parameter:
`
2.3.0 :007 >   params
=> <ActionController::Parameters {"stuff"=>"%$\#@", "page"=>{"title"=>"title", "body"=>"body", "slug"=>"slug", "is_admin"=>"true"}} permitted: false>
`
Before we can use these parameters to create a model object, we're going to need to indicate which parameters are required to be present, so that requests without them can be rejected.
We'll also need to indicate which parameters are permitted, so that other, possibly malicious parameters can be discarded.

The `require` method indicates a parameter that's required.
So, we'll call require with the symbol :page.
`
2.3.0 :008 > params.require(:page)
=> <ActionController::Parameters {"title"=>"title", "body"=>"body", "slug"=>"slug", "is_admin"=>"true"} permitted: false>
`
The require method returns the value of the parameter being required, which in this case is another ActionController::Parameters object.

The `permit` method takes the names of one or more parameters that are permitted.
Let's try calling permit on this parameters object, to indicate which parameters are permitted (and to discard that unwanted is_admin parameter).
We'll chain the methods together, calling permit directly on the return value of require.
`
2.3.0 :009 > params.require(:page).permit(:title)
=> <ActionController::Parameters {"title"=>"title"} permitted: true>
`
We got back a new parameters object.
It contains only the title parameter, since that was the only one we permitted.
And notice that the permitted attribute of the object is true this time.
That means we can use it to create a new model object.

Let's try that out.
We'll take the same command, and pass the result to a call to Page.new...
`
2.3.0 :010 > Page.new(params.require(:page).permit(:title))
=> #<Page id: nil, title: "title", body: nil, slug: nil, created_at: nil, updated_at: nil>
`
Instead of an error, we get a new Page object back.
And because we permitted the title parameter, the Page object's title attribute is set.

## Student's Notes

__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  ...

  def create
    #@page = Page.new(params)
    render text: params.to_json
  end
end

__bin/rails c__
irb(main):002:1* params = ActionController::Parameters.new(
irb(main):003:1*   stuf: "%$#@",
irb(main):004:1*   page: {title: "title", body: "body", slug: "slug", is_admin: "true"}
irb(main):005:0> )
=> <ActionController::Parameters {"stuf"=>"%$\#@", "page"=>{"title"=>"title", "body"=>"body", "slug"=>"slug", "is_admin"=>"true"}} permitted: >

__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  ...

  def create
    page_params = params.require(:page).permit(:title, :body, :slug)
    @page = Page.new(page_params)
    @page.save
    redirect_to @page
  end
end

# Controller Action to Create Pets

**Challenge Task 1 of 5**

We've got parameters like this coming in from a POST request:
`
{
  ...,
  "pet"=>{"name"=>"Jessie"},
  "commit"=>"Create Pet",
  ...
}
`
We need to set the controller's create method up to accept these parameters.
Start using the require method to require that the pet parameter group be present.
(You may want to assign the result value to a variable, as we'll be using that value in later steps of this challenge.)

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def new
    @pet = Pet.new
  end

  def create
    # YOUR CODE HERE
    pet_params = params.require(:pet)
  end
end

**Challenge Task 2 of 5**

Here's the full set of parameters coming in from a POST request again:

{
  ...,
  "pet"=>{"name"=>"Jessie"},
  "commit"=>"Create Pet",
  ...
}

Now, take the pet parameter group returned from require, and use the permit method on it to allow the name parameter.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def new
    @pet = Pet.new
  end

  def create
    # YOUR CODE HERE
    pet_params = params.require(:pet).permit(:name)
  end
end

**Challenge Task 3 of 5**

Create a new Pet object based on parameters returned from permit.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def new
    @pet = Pet.new
  end

  def create
    # YOUR CODE HERE
    pet_params = params.require(:pet).permit(:name)
    @pet = Pet.new(pet_params)
  end
end

**Challenge Task 4 of 5**

Save your new Pet object.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def new
    @pet = Pet.new
  end

  def create
    # YOUR CODE HERE
    pet_params = params.require(:pet).permit(:name)
    @pet = Pet.new(pet_params)
    @pet.save
  end
end

**Challenge Task 5 of 5**

Finally, pass the new Pet object to redirect_to, to redirect the browser to the show view.

___app/controllers/pets_controller.rb___
class PetsController < ApplicationController
  def show
    @pet = Pet.find(params[:id])
  end

  def new
    @pet = Pet.new
  end

  def create
    # YOUR CODE HERE
    pet_params = params.require(:pet).permit(:name)
    @pet = Pet.new(pet_params)
    @pet.save
    redirect_to @pet
  end
end
