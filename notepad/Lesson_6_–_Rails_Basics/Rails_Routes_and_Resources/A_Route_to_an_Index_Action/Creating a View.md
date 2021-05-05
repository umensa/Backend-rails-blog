# Creating a View
We've set up a route so that the user's browser request makes it to the index action method on the PagesController.
But the controller is attempting to render a view, and we haven't created one.
So the request is failing.
Let's create one now.

## Teacher's Notes

When looking for an ERB template so it can render an HTML response, Rails will look for a template file in this location:

app/views/<controller>/<action>.html.erb

...Where <controller> is the name of the current controller (with the word Controller left off), and <action> is the name of the current action method.

You can read more in the official Rails documentation.
(https://guides.rubyonrails.org/layouts_and_rendering.html#rendering-by-default-convention-over-configuration-in-action)

# Creating a View

**Quiz Question 1 of 1**
Please fill in the correct answer in each blank provided below.

To find a view template file for the PetsController's "show" action method, Rails will look in the app/views/pets/show.html.erb file.
(Fill in the subdirectory and the start of the file name.)
