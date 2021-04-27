#Generating a Migration

**Challenge Task 1 of 2**

Generate a migration to add an attribute to the Pet model.
On the command line, specify an attribute name of breed, with a type of string.
Since we're just adding one column, don't forget to name the migration in the format Add[ColumnName]To[ModelName (plural)].

	bin/rails generate migration AddBreedToPets breed:string

**Challenge Task 2 of 2**

The previous command generated this migration code in the db/migrate/ subdirectory:
`
class AddBreedToPets < ActiveRecord::Migration[5.0]
  def change
    add_column :pets, :breed, :string
  end
end`

Now, run the migration to add the new column to the database.

	bin/rails db:migrate
