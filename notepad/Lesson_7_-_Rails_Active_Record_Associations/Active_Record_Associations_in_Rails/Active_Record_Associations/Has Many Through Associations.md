# Has Many Through Associations
Here we have a new app with Subscriber and Magazine models.
We want people to be able to subscribe to multiple magazines, and we want to be able to look up all of a magazine's subscribers.
We could do this through a has_and_belongs_to_many association.
But what if we want to track additional info regarding the subscription itself, like how many months a person is subscribed to a magazine for?
has_and_belongs_to_many associations can't do that sort of thing. Instead, we can set up a has_many :through association.

## Teacher's Notes

We have a new app with Subscriber and Magazine models. We want people to be able to subscribe to multiple magazines, and we want to be able to look up all of a magazine's subscribers.

We could do this through a has_and_belongs_to_many association. We'd have a simple join table with subscriber_id and magazine_id columns that could be used to link Subscribers to Magazines. But what if we want to track additional info regarding the subscription itself, like how many months a person is subscribed to a magazine for? has_and_belongs_to_many associations can't do that sort of thing.

Instead, we could set up a has_many :through association. has_many :through basically says that one model is associated with many instances of another model through a third model. In this case, we would say that a Subscriber has many Magazines through Subscriptions.

It works a lot like a has_and_belongs_to_many association. The table for the Subscriptions model has ID fields for the two models it's joining, Subscribers and Magazines.

But in addition to the Subscriber and Magazine ID fields, it also has an ID field of its own, allowing you to look up Subscriptions independently of Subscribers or Magazines.

And because a Subscription is a model on its own, it can also have additional attributes. In has_many :through, two models are still joined by a database table, but that table also represents an entire third model.

You can **set up the app** we use in this video using the following shell commands:
`
rails new periodical
cd periodical
rails g model Subscriber name:string
rails g model Magazine title:string
bin/rails db:migrate
bin/rake db:seed
`
And you can **generate test data** using the following commands in the Rails console:

Subscriber.create(name: 'Jay')
Subscriber.create(name: 'Pasan')
Magazine.create(title: 'Ruby Reader')
Magazine.create(title: 'iOS Inspired')

**Generate Subscription model**

bin/rails g model Subscription months:integer subscriber_id:integer magazine_id:integer
bin/rails db:migrate

**Need to update model classes with associations**

class Subscription < ApplicationRecord
  belongs_to :subscriber
  belongs_to :magazine
end

class Subscriber < ApplicationRecord
  has_many :subscriptions
  has_many :magazines, through: :subscriptions
end

class Magazine < ApplicationRecord
  has_many :subscriptions
  has_many :subscribers, through: :subscriptions
end

**Create a subscription to a magazine, add to subscriber:**

subscription = Subscription.create(months: 12, magazine: Magazine.find_by(title: "Ruby Reader"))
Subscriber.find_by(name: "Jay").subscriptions << subscription

**Subscription now associated with subscriber. Show it with:**

pp Subscriber.find_by(name: "Jay").subscriptions

**Magazine also associated with subscriber, through subscription. Show it with:**

pp Subscriber.find_by(name: "Jay").magazines

**Can also auto-create subscription model record by adding magazine direct to subscriber**

Subscriber.find_by(name: "Jay").magazines << Magazine.find_by(title: "iOS Inspired")
pp Subscriber.find_by(name: "Jay").subscriptions

**Auto-created join model won't have its attributes set so you may need to update those**

pp Subscriber.find_by(name: "Jay").subscriptions.last.update(months: 6)
pp Subscriber.find_by(name: "Jay").subscriptions

There's a lot more you can do with has_many :through associations. You can learn more from the official Rails Guides.
(http://guides.rubyonrails.org/association_basics.html#the-has-many-through-association)

## Student's Notes
*set up the app*
*generate test data*
*Generate Subscription model*

> bin/rails g model Subscription months:integer subscriber_id:integer magazine_id:integer

__app/models/subscription.rb__
class Subscription < ApplicationRecord
  belongs_to :subscriber
  belongs_to :magazine
end

__app/models/subscriber.rb__
class Subscriber < ApplicationRecord
  has_many :subscriptions
  has_many :magazines, through: :subscriptions
end

__app/models/magazine.rb__
class Magazine < ApplicationRecord
  has_many :subscriptions
  has_many :subscribers, through: :subscriptions
end

> bin/rails db:migrate

> bin/rails c
   > subscription = Subscription.create(months: 12, magazine: Magazine.find_by(title: "Ruby Reader"))
   > Subscriber.find_by(name: "Jay").subscriptions << subscription
   > pp Subscriber.find_by(name: "Jay").subscriptions
   > pp Subscriber.find_by(name: "Jay").magazines

   > Subscriber.find_by(name: "Jay").magazines << Magazine.find_by(title: "iOS Inspired")
   > pp Subscriber.find_by(name: "Jay").subscriptions
   > Subscriber.find_by(name: "Jay").subscriptions.last.update(months: 6)
   > pp Subscriber.find_by(name: "Jay").subscriptions
