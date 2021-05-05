#Our First Resource
That welcome page is cool, but it's time to create some pages that are specific to your app.
And we're going to do it using JUST TWO terminal commands.
You're about to witness the power of convention over configuration.

##Techer's Notes
A "resource" is a thing that you want users to be able to perform "CRUD" operations on: to create instances of it, read data for it, update data for it, and delete it when they don't want it any more.

A Rails "scaffold" creates a model, view, and controller for a resource, all at once.

In your terminal:
`bin/rails generate scaffold Post title:string`

`bin/rails generate scaffold ModelName attribute1:type attribute2:type ...`

   * "rails" runs the Rails command
   * "generate" is the Rails subcommand we want to run.
   We ran the "server" subcommand before, and there are various other subcommands to do various other tasks.
   The "generate" subcommand will generate some source code files for us.
   * "scaffold" is the type of code we want to generate. 
   We'll look at other things we can generate later.
   * "ModelName" is the model we want to create a scaffold for.
   * Then, we add one or more attributes that we want our model objects to have. 
   These are bits of data that describe the object.

Among the files created will be one with a name like "db/migrate/[date]create_model_name.rb". 
This is a "migration file". It's responsible for creating the database table, which will store data for your objects.

If you ever get a "ActiveRecord::PendingMigrationError", in the terminal, type "bin/rails db:migrate". Your migration files will be run, and will set the database up for you.

To see new resources you've created a scaffold for, go to your browser's address bar and add "/model_name" at the end of the URL.
