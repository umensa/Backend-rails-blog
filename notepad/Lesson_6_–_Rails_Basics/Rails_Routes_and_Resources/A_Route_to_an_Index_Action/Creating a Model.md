# Creating a Model
We want our /pages path to show a list of blog pages.
But right now, our view template is just showing a static header.
So let's set our controller up to load some Page data so that we can include it in our template.

## Teacher's Notes

To run the model generator from your terminal:

`bin/rails generate model ModelName attr1:type attr2:type`

...Where ModelName is the name of the model class to create (like Post), attr1, attr2, etc. are the names of attributes (like title or body), and each type entry is the type of the attribute (like string or integer).

## Student's Notes
__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  def index
    @pages = Page.all
  end
end

# Creating a Model

**Challenge Task 1 of 1**
Here in the terminal, run the command to generate a Pet model for the vet application. Give it a single attribute, name, with a type of string.

	bin/rails generate model Pet name:string
