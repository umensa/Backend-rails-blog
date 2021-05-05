# Destroying Dependent Models
If you destroy a record that has_many associated records, by default, those associated records will be left in the database. Sometimes these are called "orphaned" records, because their parent record is gone. If you want associated records to be removed when their parent is removed, you can add the dependent: :destroy option to the has_many association in the model class.

## Teacher's Notes

If you destroy a record that has_many associated records, by default, those associated records will be left in the database. Sometimes these are called "orphaned" records, because their parent record is gone.

Right now, if we destroy a Movie, for example, Actor instances belonging to that movie will be left in the database.

If you want associated records to be removed when their parent is removed, you can add the dependent: :destroy option to the has_many association in the model class.

class Show < ApplicationRecord
  has_many :actors, as: :production, dependent: :destroy
end

class Movie < ApplicationRecord
  has_many :actors, as: :production, dependent: :destroy
end

In the future, when we destroy any Movie or Show instance, Actor instances belonging to that production will be removed as well.

## Student's Notes

> bin/rails c
   > Movie.first.destroy
   > pp Actor.all

__app/models/show.rb__
class Show < ApplicationRecord
  has_many :actors, as: :production, dependent: :destroy
end

__app/models/movie.rb__
class Movie < ApplicationRecord
  has_many :actors, as: :production, dependent: :destroy
end

> bin/rails c
   > Show.first.destroy
   > pp Actor.all
