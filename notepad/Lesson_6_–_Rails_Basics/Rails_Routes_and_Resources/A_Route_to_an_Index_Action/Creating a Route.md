# Creating a Route
Rails lets you set up "routes" for requests, so that you can send a particular request to a controller that can handle it.

## Teacher's Notes

To set up a route to the index of all Page objects, we add a line like this in config/routes.rb:
`
get '/pages', to: 'pages#index'`

In plain English, you could read this as "GET requests for the '/pages' path should go to the PagesController's 'index' method".

The result is a route like this:

	$ bin/rails routes
   		Prefix Verb   URI Pattern               Controller#Action
    	pages GET    /pages(.:format)          pages#index

You can read more about GET routes in the official Rails documentation.
(https://guides.rubyonrails.org/routing.html#connecting-urls-to-code)

## Creating a Route

**Quiz Question 1 of 4**

This is one of the two things Rails considers when routing a request.

	Rails looks at paths like /pages/1 or /posts to find the right controller and action method for that request.

**Quiz Question 2 of 4**

What are Rails routes used for?

	They direct particular requests to the particular controller that can handle them.

**Quiz Question 3 of 4**

This is one of the two things Rails considers when routing a request.

	HTTP request type

	Rails considers whether the request type is GET, POST, etc. when routing a request.

**Quiz Question 4 of 4**

In addition to the controller, what else do you have to specify when setting up the destination for a route?

    The action method to call.

    A controller usually has multiple action methods like "index", "show", "update", etc., and you have to specify which one should be called. 

# Viewing Routes

**Challenge Task 1 of 1**

Here in the terminal, run the command to view all the routes that are set up for your application.

> bin/rails routes

# Adding a Route

**Challenge Task 1 of 1**

We're back in our veterinarian app. Route all GET requests for the /pets path to the PetsController's index action method.

___routes.rb___
Rails.application.routes.draw do
  # YOUR CODE HERE
    get '/pets', to: 'pets#index'
end
