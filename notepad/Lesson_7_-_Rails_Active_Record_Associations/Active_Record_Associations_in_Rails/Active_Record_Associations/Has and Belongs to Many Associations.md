# Has and Belongs to Many Associations
Let's take a break from our blog example and look at another app, a discussion forum app.
We have two models in this app: a User model, and a Forum model.
We want a user to be able to join many forums so they can participate in discussions, but each forum is also going to have many users, because you can't really have discussions in a forum that has just one user.

## Teacher's Notes

You can set up your own version of the forum app used in this video with the following commands:

`rails new community
cd community
rails g model User name:string nickname:string
rails g model Forum name:string public:boolean
bin/rails db:migrate
bin/rake db:seed`

To load some sample data, run the following in the Rails console:

User.create(id: 1, name: 'Jay', nickname: 'dadjokes')
User.create(id: 2, name: 'Pasan', nickname: 'pasanpr')
User.create(id: 5, name: 'Alena', nickname: 'sketchings')
Forum.create(id: 1, name: 'Ruby', public: true)
Forum.create(id: 3, name: 'PHP', public: true)
Forum.create(id: 4, name: 'iOS', public: true)
Forum.create(id: 6, name: 'SQL', public: true)

We want a user to be able to join many forums so they can participate in discussions, but each forum is also going to have many users, because you can't really have discussions in a forum that has just one user.

So we can't just add a has_many :forums association to the User class and a belongs_to :user association to the Forum class. Doing so would allow us to associate many forums with a user, but not many users with a forum.

Instead, we'll need to set up a so-called "join table" in the database where each record has references to both a user_id and a forum_id. This allows us to link a User to multiple Forums and a Forum to multiple users, by adding records to the database. In database terms this is referred to as a "many to many relationship". You can learn more here. The relationship between the User and Forum models is known as a has_and_belongs_to_many association.

    To create the join table: bin/rails g migration CreateJoinTableUsersForums users forums
    That migration name is also somewhat magical. Because it contains "JoinTable", Rails adds a call to the create_join_table method within the resulting migration code:

class CreateJoinTableUsersForums < ActiveRecord::Migration[5.0]
  def change
    create_join_table :users, :forums do |t|
      # t.index [:user_id, :forum_id]
      # t.index [:forum_id, :user_id]
    end
  end
end

    If you use a different migration name it will still work, as long as you manually add this code.
    The calls to index on the migration table object will add indexes to the table, which will speed up database lookups. Go ahead and uncomment them.
    Active Record doesn't know to use the join table to associate the two models
        Need to use has_and_belongs_to_many method in the model classes

class User < ApplicationRecord
  has_and_belongs_to_many :forums
end

class Forum < ApplicationRecord
  has_and_belongs_to_many :users
end

Now, we can add forums to a user:

2.3.0 :001 > user = User.find_by(name: "Jay")
 => #<User id: 1, name: "Jay", nickname: "dadjokes", created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">
2.3.0 :002 > user.forums << Forum.find_by(name: "Ruby")
2.3.0 :004 > user.forums << Forum.find_by(name: "SQL")
 => #<ActiveRecord::Associations::CollectionProxy [#<Forum id: 1, name: "Ruby", public: true, created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">, #<Forum id: 6, name: "SQL", public: true, created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">]>
2.3.0 :009 > pp user.forums
[#<Forum:0x007fcc6e53bd70
  id: 1,
  name: "Ruby",
  public: true,
  created_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00,
  updated_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00>,
 #<Forum:0x007fcc6e53bc30
  id: 6,
  name: "SQL",
  public: true,
  created_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00,
  updated_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00>]
 => #<ActiveRecord::Associations::CollectionProxy [#<Forum id: 1, name: "Ruby", public: true, created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">, #<Forum id: 6, name: "SQL", public: true, created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">]>
2.3.0 :005 > user = User.find_by(name: "Pasan")
 => #<User id: 2, name: "Pasan", nickname: "pasanpr", created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">
2.3.0 :006 > user.forums << Forum.find_by(name: "iOS")
 => #<ActiveRecord::Associations::CollectionProxy [#<Forum id: 4, name: "iOS", public: true, created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">]>
2.3.0 :007 > pp user.forums
[#<Forum:0x007fcc6b0023c0
  id: 4,
  name: "iOS",
  public: true,
  created_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00,
  updated_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00>]
 => #<ActiveRecord::Associations::CollectionProxy [#<Forum id: 4, name: "iOS", public: true, created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">]>

We can also look up users that belong to a forum:

2.3.0 :011 > pp Forum.find_by(name: "Ruby").users

[#<User:0x007fcc6e4b28b8
  id: 1,
  name: "Jay",
  nickname: "dadjokes",
  created_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00,
  updated_at: Sun, 01 Oct 2017 03:40:29 UTC +00:00>]
 => #<ActiveRecord::Associations::CollectionProxy [#<User id: 1, name: "Jay", nickname: "dadjokes", created_at: "2017-10-01 03:40:29", updated_at: "2017-10-01 03:40:29">]>
2.3.0 :015 > pp ActiveRecord::Base.connection.execute "select * from forums_users"
[{"user_id"=>1, "forum_id"=>1, 0=>1, 1=>1},
 {"user_id"=>1, "forum_id"=>6, 0=>1, 1=>6},
 {"user_id"=>2, "forum_id"=>4, 0=>2, 1=>4}]
 => [{"user_id"=>1, "forum_id"=>1, 0=>1, 1=>1}, {"user_id"=>1, "forum_id"=>6, 0=>1, 1=>6}, {"user_id"=>2, "forum_id"=>4, 0=>2, 1=>4}]

## Student's Notes

> bin/rails g migration CreateJoinTableUsersForums users forums

__db/migrate/****_create_join_table_users_forums.rb__
class CreateJoinTableUsersForums < ActiveRecord::Migration[5.0]
  def change
    create_join_table :users, :forums do |t|
       t.index [:user_id, :forum_id]
       t.index [:forum_id, :user_id]
    end
  end
end

> bin/rails db:migrate

__app/models/user.rb__
class User < ApplicationRecord
  has_and_belongs_to_many :forums
end

__app/models/forum.rb__
class Forum < ApplicationRecord
  has_and_belongs_to_many :users
end

> bin/rails c
   > user = User.find_by(name: "Jay")
   > user.forums << Forum.find_by(name: "Ruby")
   > user.forums << Forum.find_by(name: "SQL")
   > pp user.forums

   > user = User.find_by(name: "Pasan")
   > user.forums << Forum.find_by(name: "iOS")
   > pp user.forums

   > pp Forum.find_by(name: "Ruby").users
   > pp ActiveRecord::Base.connection.execute "select * from forums_users"
