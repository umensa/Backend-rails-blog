# workshop

# Missing Components - DB Tables
What to do about a MigrationPendingError.

*To complete a request, Rails needs:*

   * Database table
   * Route in config/routes.rb
   * A controller action

## Student's Notes

_Create Owner Model_
> $ bin/rails generate model Owner name:string

__app/models/owner.rb__
class Owner < ApplicationRecord
end

___localhost:3000/owners___
**ActiveRecord::PendingMigrationError**
Migration are pending.

> $ bin/rails db:migrate

___localhost:3000/owners___
**Routing Error**
No route matches [GET] "/owners"

__db/migrate/0123456789_create_owners.rb__
class CreateOwners < ActiveRecord::Migration[5.0]
  def change
    create_table :posts do |t|
      t.string :name

      t.timestamps
    end
  end
end

# Missing Components - Routes
We just updated our database, and we're still trying to load the list of Owners in our browser.
But now we have another problem.
It's reporting a routing error: "No route matches [GET] '/owners'".

## Teacher's Notes
If you'd like to know more about the HTTP protocol, check out our HTTP Basics course.

## Student's Notes

___localhost:3000/owners___
**Routing Error**
No route matches [GET] "/owners"

__config/routes.rb__
Rails.application.routes.draw do
  resources :pets
  get '/owners', to: 'owners#index'
end

___localhost:3000/owners___
**Routing Error**
uninitialized constant OwnersController

# Missing Components - Controllers
We set up a route to the OwnersController here in `config/routes.rb`, but we haven't created the controller class within the `controllers/` directory yet.
Let's do that now.

## Student's Notes

> rails generate controller Owners index

__app/controllers/owners_controller.rb__
class OwnersController < ApplicationController
  def index
  end
end

___localhost:3000/owners___
**Owners#index**
	find me in app/views/owners/index.html.erb

*To complete a request, Rails needs:*

   * Database table
   * Route in config/routes.rb
   * A controller action

# Mistakes in Code
Sometimes errors are caused by a typo in your code.

## Student's Notes

___localhost:3000/pets___
**SyntaxError in PetsController#index**
/../app/models/pet.rb:1: syntax error, unexpected '>' class Pet > ApplicationRecord^

__app/models/pet.rb__
class Pet < ApplicationRecord
end

___localhost:3000/pets___
**SyntaxError in PetsController#index**
/../app/controller/pets_controller.rb:56: syntax error, unexpected end-of-input, expecting keyword_end

__app/controller/pets_controller.rb__
...
def new
	@pet = Pet.new
end
...

___localhost:3000/pets/1___
**NameError in Pets#show**
Showing /../app/views/pets/show.html.erb where line #5 raised:
undefined local variable or method `pet` for #<#<Class:0x..>
Did you mean @pet

__app/views/pets/show.html.erb__
..
	<%= @pet.name %>
...

# View Problems - Unwanted Elements
There's something being displayed on your page, and you don't want it there, but you don't know where it's coming from.
Here's how to find the source.

## Student's Notes

*Typical components of a Rails view*
   * Application-wide layout
   * Page template
   * One or more partials

__app/views/layouts/application.html.erb__
<!DOCTYPE html>
<html>
  <head>
    <title>Vet</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>

__app/views/pets/edit.html.erb__
..
<%= render 'form', page: @page %>
.. # no debug for the string

__ app/views/pets/_form.html.erb_
`# <%= pet %>`

<%= form_for(pet) do |f| %>
	<% if pet.errors.any? %>
		<div id="error_explanation">
			<h2><%= pluralize(pet.errors.count, "error") %> prohibited this pet from being ..</h2>

			<ul>
			<% pet.error.full_message.each do |message| %>
				<li><%= message %></li>
			<% end %>
			</ul>
		</div>
	<% end %>
	...
<% end %>

# View Problems - Incorrect Name
What if you've added a view, and it's not being found?

## Student's Notes

___localhost:3000/pets/3___
**Template is missing**
Missing template pets/edits, application/edits with {:locale=>[:en], :formats=>[:html], :variants=>[], :handlers=>[:raw, :erb, :html, :builder, :ruby, :coffee, :jbuilder]}.
Searched in: * "/../app/views"

__app/controllers/pets_controller.rb__
..
def update
	if @pet.update(pet_params)
		redirect_to @pet, notice: 'Pet was successfully updated.'
	else
		render :edit `#edits`
	end
end
..

# Database Issues
We'll show you how to troubleshoot problems accessing your database.
We'll also show you how to use the Rails Logger as a general debugging tool.

## Teacher's Notes
You can read more about the Rails Logger on the Rails Guides site.
(https://guides.rubyonrails.org/debugging_rails_applications.html#the-logger)

## Student's Notes

___localhost:3000/pets/3___
**ActiveRecord::RecordNotFound in PetsController#show**
Couldn't find Pet with 'id'=3

__app/controllers/pets_controller.rb__
class PetsController < ApplicationController
	before_action :set_pet, only: [:edit, :update, :destroy]
	...
	def show
		@pet = Pet.find(params[:id])
	rescue ActiveRecord::RecordNotFound
		flash[:notice] = "We couldn't find that Pet."
		redirect_to action: :index
	end
	...
end

___localhost:3000/pets/2/edit___
**ActiveRecord::RecordNotFound in PetsController#edit**
Couldn't find Pet with 'id'=

__app/controllers/pets_controller.rb__
..
`# GET /pet/1/edit`
def edit
	`# logger.info("The :pet parameter is: #{params[:pet]}")`
	@pet = Pet.find(params[:id]) ` # not :pet`
end
...

# General Tips
We want to leave you with a few general tips that aren't specific to Rails, but will help keep bugs from getting out of control.

## Teacher's Notes
You can learn more about testing your Rails apps here.
(https://guides.rubyonrails.org/testing.html)

Want to learn more about version control using Git? Check out our Git Basics course.

## Student's Notes

**General Tips**

   * Make sure you're writing automated tests or specs
   * Make your changes in small batches when yu can, and test them frequently
   * Use a version control system, like Git
   * Don't be afraid to use your editor's "Find in Files" feature to search all the files in your project for a particular string
