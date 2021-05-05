#Creating a Rails App
Let's create a new Rails app, and then test it out.

##Techer's Notes
Type "rails new", followed by the name of the app you want to create.
To run a server, change into the new app's directory, then type "bin/rails server", or on Windows, type "ruby bin\rails server".

`rails new appname
cd appname
bin/rails server`

Rails will begin logging messages to your terminal. You should see a URL like "http://localhost:3000"; this is the address where the server is running.
Paste that URL into your browser to view your app's welcome page.

To stop the server later, return to your terminal window and press Ctrl-C.

An important detail for Windows users: 
Anywhere in the upcoming courses that you see me type `bin/rails`, or `bin/` followed by any other command, you need to change the command a little bit so that it works on your system.
Just replace the `bin/` with `ruby bin\`.
You need to do this because, unlike Macs and Linux machines, Windows can't run Ruby scripts directly by default; they have to be run through the "ruby" command.
