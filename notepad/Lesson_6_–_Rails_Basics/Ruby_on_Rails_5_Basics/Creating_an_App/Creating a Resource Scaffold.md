#Creating a Resource Scaffold

**Challenge Task 1 of 2**

We're back in the directory for our vet app... Generate a scaffold for a `Pet` resource.
Pet instances should have a single attribute, `name`, with a type of `string`.

	bin/rails generate scaffold Pet name:string

**Challenge Task 2 of 2**

We tried to run the Rails server after generating the scaffold, but we're getting an ActiveRecord::PendingMigrationError.
Enter the command that will fix the error and get our server running again.

	bin/rails db:migrate
