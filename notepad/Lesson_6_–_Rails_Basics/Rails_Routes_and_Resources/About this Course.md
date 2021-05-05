# About this Course
You've seen how to create a Rails resource using a scaffold.
But scaffolds don't offer flexibility in how a resource is set up.
Let's create a resource totally by hand to see how it's put together.
Along the way, we'll learn another important component of Rails: routes.

## What you'll learn

   * Routes
   * Models
   * Views
   * Controllers

## A Route to an Index Action
In the first stage, we'll read all Page records in the database and display their titles in a list.
(Since we won't yet have a form for adding Pages, we'll have to add some via the Rails console.)
This first stage will be the most involved, since we'll need to set up a route, a controller, a view, AND a model for our Pages.

*14 steps*

__Introduction__
2:03

__Creating a Route__
4:45

__Creating a Route__
4 questions

__Viewing Routes__
1 objective

__Adding a Route__
1 objective

__Creating a Controller__
2:39

__Creating a Controller__
1 objective

__Creating a View__
1:29

__Creating a View__
1 question

__Creating a Model__
3:32

__Creating a Model__
1 objective

__Adding Records via Rails Console__
3:17

__Populating the View__
8:57

__Populating the View__
2 objectives

##  A Route to a Read Action
Users can view a list of all our page titles, but they can't view the content of single Pages yet.
For our Posts resource, they can click a link on the list of all Posts to view an individual post.
Let's set up links to view single Pages as well.

*9 steps*

__Linking to Pages__
3:56

__Linking to Model Objects__
1 objective

__Set Up a URL Parameter__
1 objective

__Path Helpers__
1:38

__Path Helpers__
1 objective

__Finding a Page__
2:55

__Finding a Model Object__
1 objective

__Creating a Show View__
2:01

__Creating a Show View__
1 objective

##  Routes to Create Actions
Our users can view a list of all Pages.
They can click a link to view an individual Page.
What they CAN'T do right now is create new pages; we had to go into the Rails console to do that.
Our next task is to set up a form so that it's easy for our USERS to create Pages, too.


*10 steps*

__Route for New Pages__
3:08

__Route for New Pets__
1 objective

__Controller Action for New Pages__
1:48

__View for New Pages__
5:42

__Controller Action for New Pets__
1 objective

__View for New Pets__
4 objectives

__Route to Create Pages__
1:18

__Route to Create Pets__
1 objective

__Controller Action to Create Pages__
11:27

__Controller Action to Create Pets__
5 objectives

##  Routes to Update Actions
Now our users can create a new Page.
But they'd better get it right the first time, because right now they can't go back and change what they've entered.

Maybe we should fix that.
Let's give them a form to allow them to update existing Pages.


*6 steps*

__An Edit Route__
6:24

__An Edit Route__
1 objective

__An Edit Form__
5:31

__Moving the Pet Form to a Partial__
5 objectives

__An Update Action__
5:52

__An Update Action__
5 objectives

##  A Route to a Delete Action
For every resource you create, there may come a time when you don't want it any more.
So, let's allow our users to delete Pages.


*6 steps*

__Deleting Pages__
5:30

__A Delete Action__
3 objectives

__Rails Resources__
3:50

__A Pets Resource__
1 objective

__Filters__
3:41

__Summary__
0:45
