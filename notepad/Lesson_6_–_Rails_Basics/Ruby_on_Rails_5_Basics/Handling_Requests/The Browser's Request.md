#The Browser's Request
We've set up our posts resource, and we're able to view posts in our browser.
But what's actually happening when you load that URL?

##Techer's Notes
Here's an overview of how Rails handles a request.

   * Rails looks at the request, to figure out which code should handle it.
   * The request gets routed to an action method on a "controller".
   * The controller loads the resource in from database using a "model class".
   * The controller renders a "view" using the model data, to generate the response content.

To retrieve the URL "http://localhost:3000/posts", your browser sends an HTTP "GET" request.

   * Your browser uses a communication standard called HyperText Transfer Protocol, or HTTP, to talk to web servers.
   That's the "http:" at the start of the URL.
   * "localhost:3000" is the host and port.
   * "/posts" is the path to the resource you want.

When you press Enter to load the URL, your browser sends an HTTP GET request - it gets the page.
(There are other HTTP request types like POST and DELETE, too. We'll look at those later.)
If you'd like to learn more about the HTTP protocol, check out the HTTP Basics course.

If we switch to the terminal and look in the log, we can see where Rails received the request, and how it was handled.
`
Started GET "/posts" for ::1 at 2016-05-28 12:37:31 -0700
Processing by PostsController#index as HTML
  Rendering posts/index.html.erb within layouts/application
  Post Load (0.1ms)  SELECT "posts".* FROM "posts"
  Rendered posts/index.html.erb within layouts/application (1.6ms)
Completed 200 OK in 23ms (Views: 20.2ms | ActiveRecord: 0.1ms)
`
This log shows where Rails recieved the request, passed it to a controller, loaded some model data, and rendered a view.
