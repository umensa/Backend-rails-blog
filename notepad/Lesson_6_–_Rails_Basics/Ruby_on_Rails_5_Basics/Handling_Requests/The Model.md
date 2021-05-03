#The Model
The model is responsible for storing and retrieving data from users of your app.

**Quiz Question 1 of 5**
What is the responsibility of Rails models?

	storing and retrieving data

**Quiz Question 2 of 5**
Please fill in the correct answer in each blank provided below.

	Rails generates code for new model classes in the app/ models subdirectory.

**Quiz Question 3 of 5**
The "all" class method is just one of many methods you can call on model classes. Where do these methods come from in Rails 5?

	    They're inherited from the ApplicationRecord class.

	Almost no methods are defined directly on your application's model classes. 
	Instead, they're inherited from a superclass. 

**Quiz Question 4 of 5**
When you call a model method, Rails sends the database a command in this language, used for communicating with databases.

	Databases don't speak Ruby.
	When you need data from a database, you send it a "query" using SQL. 

**Quiz Question 5 of 5**
When you call the "all" method on a model class, what happens to the database records?

	Each record is converted to an instance of the model class.

	 If you call Post.all, you'll get a collection of Post objects back. 
