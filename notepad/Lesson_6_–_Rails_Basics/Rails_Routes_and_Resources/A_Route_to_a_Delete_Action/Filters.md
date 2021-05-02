# Filters
At the top of your controller class, outside of any instance methods, you can call the before_action method, and pass it a symbol with the name of a method.
With this set up, the controller will call that method before running any action method.

## Student's Notes

__app/controllers/pages_controller.rb__
class PagesController < ApplicationController
  before_action :set_page, only: [:show, :edit, :update, :destroy]
  def index
    @pages = Page.all
  end

  def show
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
  end

  def update
    @page.update(page_params)
    redirect_to @page
  end

  def destroy
    @page.destroy
    redirect_to pages_path
  end

  private

    def page_params
      params.require(:page).permit(:title, :body, :slug)
    end

    def set_page
      @page = Page.find(params[:id])
    end
end
