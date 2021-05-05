# Populating the View
We've set up our controller's "index" method to load all "Page" objects into the "@pages" instance variable.
We've also created some "Page" records for it to load.
That was only part of the problem, though; we still don't see any page data.
That's because we haven't set up the our view template to display the pages we've loaded.
To do that, we're going to use ERB to embed some Ruby code into our HTML.

## Teacher's Notes

Most text in an ERB template is copied to the output verbatim.

`<p>I'll appear in the output exactly as I do here.</p>`

But Ruby code within ERB tags gets evaluated instead of being copied directly to the output.

Code within output ERB tags (<%= %>) is evaluated, and the result is embedded into the output. This code will output the current time:

`<p>The current time is: <%= Time.now %></p>`

Code within regular ERB tags (<% %>, without an equals sign) is also evaluated, but is not included directly in the output. It can be used to influence the result of output tags.

If you place a conditional within regular tags, text within the conditional will only be output if the condition is true. This code will include You passed! in the output:
`
<% grade = 97 %>
<% if grade > 60 %>
  You passed!
<% end %>
`
This code will not:
`
<% grade = 54 %>
<% if grade > 60 %>
  You passed!
<% end %>
`
If you place a loop in regular ERB tags, text within the loop will be output repeatedly. This code will output 4 <p> elements with the text 0 fish, 1 fish, 2 fish, and 3 fish:
`
<% 4.times do |index| %>
  <p><%= index %> fish</p>
<% end %>
`
Assuming @pages contains a collection of Page objects, this code will output the title of each Page:
`
<% @pages.each do |page| %>
  <p>
    <%= page.title %>
  </p>
<% end %>
`
Want to learn about looping over the values in a collection with each? Check out our Ruby Loops course.

# Populating the View

**Challenge Task 1 of 2**

The index action method on the PetsController includes the following code:

def index
  @pets = Pet.all
end

We need to populate our page with the list of pets. For this first task, use the each method in ERB tags to loop over each of the Pet objects.

___app/views/pets/index.html.erb___
<% @pets.each do |pet| %>
<p><%= pet %></p>
<% end %>

**Challenge Task 2 of 2**

Now we need to output HTML <p> elements with the name attribute of each pet. Within the each block, add <p></p> HTML tags. Between those tags, embed the name attribute of the current Pet.

___app/views/pets/index.html.erb___
<% @pets.each do |pet| %>
<p><%= pet.name %></p>
<% end %>