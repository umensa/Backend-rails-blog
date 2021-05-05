# Controller Action for New Pages
We're trying to set up an HTML form for new Page objects.
We've defined a route for the /pages/new path that directs to the new method on PagesController.
Now we just need to define that method.

## Student's Notes

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
end
