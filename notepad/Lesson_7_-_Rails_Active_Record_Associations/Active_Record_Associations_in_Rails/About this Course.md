# About this Course
Most of your Rails models are going to be connected to other models in some way.
An Author has many Articles, and each Article belongs to an Author.
A Doctor has many Patients, and a Patient may have many Doctors as well.
Rails uses associations to make it easy to track these relationships in your database.

**What you'll learn**

   * has_many
   * belongs_to
   * has_one
   * has_and_belongs_to_many
   * has_many :through

## Active Record Associations 
Our blog app doesn't allow users to tell us how awesome our posts are.
This situation is, of course, unacceptable.
So we're going to need a comments system.
We need to be able to associate comments with a particular post.


*11 steps*

__Introduction__
2:52

__Has Many Associations__
8:53

___Has Many___
1 objective

___Association Methods___
1 objective

___A "Has Many" Migration___
1 objective

__Belongs To Associations__
2:20

___"Belongs To" Associations___
1 objective

__Variations on Foreign Key Migrations__
6:31

__Has and Belongs to Many Associations__
6:32
> https://github.com/Code-the-Dream-School/Backend-community
*Community Application*
   - This repository contains the framework for the application called "community" in the following Treehouse video for Active Record Associations in Rails: https://teamtreehouse.com/library/has-and-belongs-to-many-associations.
   - You should create a git branch called community and make your changes there.
   - When you are done with the application, because you have completed all the changes from the Treehouse videos, you can git add, commit, and push your changes and make a pull request.
The first thing you will have to do is to complete the setup.
This is described in the Teacher's Notes at the link above.
You do not do the `rails new` command, as that has been done for you.
You start with the `rails g model User` command as described in the notes and complete the directions in those notes and in the video.
This application is also used and modified in the following video: https://teamtreehouse.com/library/has-one-associations .

__Has Many Through Associations__
7:26
> https://github.com/Code-the-Dream-School/Backend-periodical
*Periodical*
   - This repository contains the framework for the application called "periodical" in the following Treehouse video for Active Record Associations in Rails: https://teamtreehouse.com/library/has-many-through-associations.
   - You should create a git branch called periodical and make your changes there.
   - When you are done with the application, because you have completed all the changes from the Treehouse videos, you can git add, commit, and push your changes and make a pull request.
The first thing you will have to do is to complete the setup.
This is described in the Teacher's Notes at the link above.
You do not do the `rails new` command, as that has been done for you.
You start with the `rails g model Subscriber` command as described in the notes and complete the directions in those notes and in the video.

__Has One Associations__
3:39
*Community Application*

## Using Associations in Your App
Working with associated models in your controllers won't be much different from working with them in the Rails console.
But rendering them in your views and representing the association in your routes might take a little more work.
We'll cover those details and more in this stage.


*8 steps*

__Rendering Associated Models in Views__
3:15

__Rendering Associated Models Using Partials__
4:29

___Rendering Collections___
1 objective

__Nested Routes and Resources__
4:31

___Nested Routes and Resources___
1 objective

__Creating an Associated Record__
8:41

__Updating an Associated Record__
6:40

__Deleting an Associated Record__
3:04

## More Association Options
When it comes down to it, associations really just make some changes to the SQL queries that Active Record runs on your database.
If you want, Rails gives you the power to take more control over those queries.
In this stage, we'll look at some options for doing that.


*6 steps*

__Polymorphic Options__
7:37
> https://github.com/Code-the-Dream-School/Backend-mdb
*Movie Database*
   - This repository contains the framework for the movie database application called "mdb" in the following Treehouse video for Active Record Associations in Rails: https://teamtreehouse.com/library/polymorphic-options.
   - You should create a git branch called mdb and make your changes there.
   When you are done with the application, because you have completed all the changes from the Treehouse videos, you can git add, commit, and push your changes and make a pull request.
The first thing you will have to do is to complete the setup.
This is described in the Teacher's Notes at the link above.
You do not do the `rails new` command, as that has been done for you. You start with the `rails g scaffold Movie` command as described in the notes and complete the directions in those notes and in the video.

___A Migration for a Polymorphic Association___
1 objective

___Polymorphic "Has Many" Associations___
1 objective

___Polymorphic "Belongs To" Associations___
1 objective

__Destroying Dependent Models__
1:27

__More Association Methods__
3:46
