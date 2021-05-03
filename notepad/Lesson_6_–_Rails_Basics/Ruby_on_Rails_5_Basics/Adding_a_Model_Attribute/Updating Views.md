#Updating Views
Our "Post" model objects have a "body" attribute now, but that attribute doesn't show up on our site anywhere.
In order to fix this, we're going to need to update the affected views to display the "body" attribute.

##Techer's Notes


Let's open "app/views/posts/index.html.erb" in our editor. This template is creating an HTML table of all the posts and their attributes. If you want to learn more about HTML tables, see the HTML Tables course.

...
<table>
  <thead>
    <tr>
      <th>Title</th>
      <th>Body</th> <!--Add header here-->
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <!-- Process each post -->
    <% @posts.each do |post| %>
      <tr>
        <!-- The current post's title -->
        <td><%= post.title %></td>
        <!-- Add body attribute here -->
        <td><%= post.body %></td>
        <td><%= link_to 'Show', post %></td>
...

If we save our work and reload the page, we'll see a body for the post that we edited in the Rails console.
We'll see blank bodies for the other posts (since they're still blank in the database).

Now, let's add the body attribute in the view for a single post.
Edit the "app/views/posts/show.html.erb" file.

...
<!-- Existing post title code here -->
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<!-- Add a new HTML paragraph tag... -->
<p>
  <!-- With the post body embedded inside. -->
  <%= @post.body %>
</p>
...

When we edit an existing post, or create a new post, we're not given a field to edit the body attribute.
We want to fix that next.
But when we edit the ERB template at "app/views/posts/edit.html.erb", we don't see HTML to render a form directly.
The same is true for "app/views/posts/new.html.erb".
Instead, we see a call to the "render" method with an argument of "form".

`<%= render 'form', post: @post %>`

When "render" is called from either of these templates, it looks up a "partial".
"Partial" is short for "partial view".
And it's this partial that contains the HTML code for the form.

You can take the HTML code that's identical between two templates, and move it to a partial view.
Then, each template that needs that code can render the partial, and the partial's code will be included in the template's code.
When you need to make a change, you only have to update the partial.
Any changes you make will immediately be visible in all the views that use that partial.

So both the edit post page and the new post page include a call to render a partial called "form". If we look at the log, we'll see it's been showing us the step where it renders the partial all along. Within both the "edit" and "new" requests, we'll see `"Rendered posts/_form.html.erb"`.

   * The underscore at the start of the file name indicates that a file holds a partial template.
   * When calling "render", you can leave the underscore and the ".html.erb" extension off.
   Rails can add those automatically.
   That leaves just "render 'form'".
   * Following the name of the partial is a hash that sets up local variables for use within the partial.
   So this will make the `@post` instance variable available within the partial as the "post" local variable.

Let's open the partial file to see what it contains.
It's at "app/views/posts/_form.html.erb".
`
<%= form_for(post) do |f| %>
  <!-- Trimming error display code -->
  <!-- Existing title field -->
  <div class="field">
    <%= f.label :title %>
    <%= f.text_field :title %>
  </div>
``
  <!-- Create a new div element to hold body -->
  <div class="field">
    <!-- The label that appears next to field -->
    <%= f.label :body %>
    <!-- The field itself -->
    <!-- Using text_area instead of text_field
    <!-- makes it bigger -->
    <%= f.text_area :body %>
  </div>
``
  <div class="actions">
    <%= f.submit %>
  </div>
<% end %>
`
   * We can see that it takes the "post" object we passed in, and renders an HTML form for it.
   * The "f" variable here will hold a Ruby object representing the HTML form. We can call methods on that object to add elements to the HTML form.
