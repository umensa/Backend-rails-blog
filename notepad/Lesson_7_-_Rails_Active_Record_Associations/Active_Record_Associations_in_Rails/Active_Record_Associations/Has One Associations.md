# Has One Associations
Some tables in your database will have a tendency to grow in number of columns over time.
Eventually, the number of columns can become unwieldy.
When this happens, it may be a good idea to move the less-frequently-used columns to a separate table, and have them tracked by a separate Rails model.

## Teacher's Notes


Some tables in your database will have a tendency to grow in number of columns over time. Eventually, the number of columns can become unwieldy. When this happens, it may be a good idea to move the less-frequently-used columns to a separate table, and have them tracked by a separate Rails model.

A foreign key in the original table references the primary key of the new table. This works just like a has_many association, except that a record in the original table will only ever be associated with one record in the new table. So Active Record calls this a has_one association.

We're back in our forum app, and we want to create a Profile model to hold some of our user data. The User model class will have a has_one association with the Profile class.

We can generate the Profile model like this:

bin/rails g model Profile user:references twitter:string github:string

That creates this migration:

class CreateProfiles < ActiveRecord::Migration[5.0]
  def change
    create_table :profiles do |t|
      t.references :user, foreign_key: true
      t.string :twitter
      t.string :github

      t.timestamps
    end
  end
end

Then we need to declare that a User has_one Profile:

class User < ApplicationRecord
  has_and_belongs_to_many :forums
  has_one :profile
end

With that done, we can set up a Profile for a User in the Rails console:

user = User.find_by(name: "Jay")
user.profile
user.create_profile(twitter: "jaymcgavren", github: "jaymcgavren")
pp User.first
pp User.first.profile

    [Rails Guides: has_one associations](http://guides.rubyonrails.org/association_basics.html#the-has-one-association)
    Rails Guides: has_one association methods

## Student's Notes

> bin/rails g model Profile user:references twitter:string github:string

__db/migrate/****_create_profiles.rb__
class CreateProfiles < ActiveRecord::Migration[5.0]
  def change
    create_table :profiles do |t|
      t.references :user, foreign_key: true
      t.string :twitter
      t.string :github

      t.timestamps
    end
  end
end

> bin/rails db:migrate

__app/models/user.rb__
class User < ApplicationRecord
  has_and_belongs_to_many :forums
  has_one :profile
end

> bin/rails c
   > user = User.find_by(name: "Jay")
   > user.profile
   	=> nil
   > user.create_profile(twitter: "jaymcgavren", github: "jaymcgavren")
   > pp User.first
   > pp User.first.profile
