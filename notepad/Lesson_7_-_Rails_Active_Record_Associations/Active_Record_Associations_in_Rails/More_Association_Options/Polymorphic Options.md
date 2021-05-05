# Polymorphic Options
Polymorphic belongs_to associations allow a model to belong to more than one type of other model.

## Teacher's Notes
You can set up a movie database app like we use in the video with these terminal commands:

rails new mdb
cd mdb
bin/rails g scaffold Movie title:string duration:integer
bin/rails g scaffold Show title:string episodes:integer
bin/rails g scaffold Actor name:string
bin/rails g migration AddProductionToActor production_id:integer production_type:string
bin/rails db:migrate

If you prefer, there's an alternate syntax for adding the _ id and _ type reference fields to the migration:

bin/rails g migration AddProductionToActor production:references{polymorphic}

Now we need to set up the polymorphic association in the model classes:

class Movie < ApplicationRecord
  has_many :actors, as: :production
end

class Show < ApplicationRecord
  has_many :actors, as: :production
end

class Actor < ApplicationRecord
  belongs_to :production, polymorphic: true
end

With all that set up, you can add an Actor to either a Show or a Movie in the Rails console:

show = Show.create(title: "Game of Thrones")
show.actors
show.actors.create(name: "Peter Dinklage")
show.actors.create(name: "Lena Headey")
pp Show.first.actors
Actor.first.production
movie = Movie.create(title: "Fight Club")
movie.actors.create(name: "Brad Pitt")
movie.actors.create(name: "Edward Norton")
Movie.first.actors
pp Actor.all

You can read more about using polymorphic associations within your app here. (https://guides.rubyonrails.org/association_basics.html#polymorphic-associations)

## Student's Notes

> bin/rails g scaffold Movie title:string duration:integer
> bin/rails g scaffold Show title:string episodes:integer
> bin/rails g scaffold Actor name:string
> bin/rails g migration AddProductionToActor production_id:integer production_type:string
> bin/rails db:migrate

__app/models/movies.rb__
class Movie < ApplicationRecord
  has_many :actors, as: :production
end
__app/models/show.rb__
class Movie < ApplicationRecord
  has_many :actors, as: :production
end

__app/models/actor.rb__
class Actor < ApplicationRecord
  belongs_to :production, polymorphic: true
end

> bin/rails c
   > show = Show.create(title: "Game of Thrones")
   > show.actors.create(name: "Peter Dinklage")
   > show.actors.create(name: "Lena Headey")

   > movie = Movie.create(title: "Fight Club")
   > movie.actors.create(name: "Brad Pitt")
   > movie.actors.create(name: "Edward Norton")

# Polymorphic "Has Many" Associations

**Challenge Task 1 of 1**

We need to be able to specify that a Part model belongs to either a Car or a Truck (which we will refer to as "vehicles"). Assume that cars and parts tables already exist. Here at the command line, generate a migration that will add vehicle_id and vehicle_type columns to the parts table.

> bin/rails g migration AddVehiclesToParts vehicle_id:integer vehicle_type:string

# Polymorphic "Has Many" Associations

**Challenge Task 1 of 1**

Update the Car and Truck model classes so that each is treated as a "vehicle" which has_many Part instances.

__models/car.rb__
class Car < ApplicationRecord

  # YOUR CODE HERE
  has_many :parts, as: :vehicle

end

__models/truck.rb__
class Truck < ApplicationRecord
  # YOUR CODE HERE
  has_many :parts, as: :vehicle
end

# Polymorphic "Belongs To" Associations

**Challenge Task 1 of 1**

Update the Part model class so that each instance belongs to a "vehicle". (The "vehicle" is a polymorphic association with either a Car or a Truck.)

__models/part.rb__
class Part < ApplicationRecord

  # YOUR CODE HERE
  belongs_to :vehicle, polymorphic: true

end
