# Creating a Show View
We're displaying some raw text for individual Page records, but we'd like to display a full HTML page.
For that we're going to need an ERB template.

## Teacher's Notes

This video shows a call to render text:, which works fine in Rails 5.0 (the recommended version to use when following along with this course).
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
  end
end

__app/views/pages/show.html.erb__
<h1><%= @page.title %></h1>
<p>
	<%= @page.body %>
</p>

# Creating a Show View

**Challenge Task 1 of 1**

The show action method on the PetsController includes the following code:

def show
  @pet = Pet.find(params[:id])
end

Add a level 1 heading (<h1>) element to the template. Within that element, embed the Pet's name attribute.

___app/views/pets/show.html.erb___
<h1><%= @pet.name %></h1>
