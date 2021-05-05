#Destroy Operations

**Challenge Task 1 of 2**

Calling Pet.all returns the following collection of records:

`#<ActiveRecord::Relation [
#<Pet id: 1, name: "Tchai", birthdate: "2016-04-26", created_at: "2016-07-28 17:37:24", updated_at: "2016-07-28 17:37:24">,
#<Pet id: 3, name: "Sassie", birthdate: "2016-04-26", created_at: "2016-07-28 17:37:45", updated_at: "2016-08-17 17:37:45">,
#<Pet id: 4, name: "Scottie", birthdate: "1983-05-17", created_at: "2016-08-17 21:19:49", updated_at: "2016-08-17 21:19:49">]`

Retrieve the Pet record with an ID of 4, and store the model object in the pet variable.

> pet = Pet.find(4)

**Challenge Task 2 of 2**

Now delete the model object that's referenced by pet.

> pet.destroy
