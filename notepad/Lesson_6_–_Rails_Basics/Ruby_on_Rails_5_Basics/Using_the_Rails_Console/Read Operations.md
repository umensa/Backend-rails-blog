#Read Operations

**Challenge Task 1 of 3**
We're in the Rails console for our vet app.
Call the method to retrieve a collection of all Pet records.

	Pet.all

**Challenge Task 2 of 3**
Now call the method to retrieve just the most recent Pet record.

	Pet.last

**Challenge Task 3 of 3**
Calling Pet.all returns the following collection of records:
`
#<ActiveRecord::Relation [
#<Pet id: 1, name: "Tchai", birthdate: "2016-04-26", created_at: "2016-07-28 17:37:24", updated_at: "2016-07-28 17:37:24">,
#<Pet id: 2, name: "Max", birthdate: "2016-04-26", created_at: "2016-07-28 17:37:45", updated_at: "2016-07-28 17:37:45">,
#<Pet id: 4, name: "Scottie", birthdate: "1983-05-17", created_at: "2016-08-17 21:19:49", updated_at: "2016-08-17 21:19:49">]`

Retrieve the record for the Pet with a name of "Max" using just its ID.

	Pet.find(2)
