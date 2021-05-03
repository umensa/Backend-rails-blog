#The Controller
The controller is responsible for handling the browser request.
It CONTROLS the model and the view to generate a response.

##Techer's Notes
When you access the list of all "Post" objects, the request gets sent to the "index" method of the "PostsController" class.

   * Rails creates the source code for controller classes in the "app/controllers/" subdirectory.
   * The "PostsController" class will be in "posts_controller.rb".
   * The request is handled by the "index" method or action (controller methods that respond to requests are sometimes called "actions").

<!-- posts_controller.rb
  def index
    @posts = Post.all
  # render template: "posts/index.html.erb", layout: "application"
  end 
-->
