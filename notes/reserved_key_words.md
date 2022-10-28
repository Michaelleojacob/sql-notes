*from: https://www.theodinproject.com/lessons/databases-databases-and-sql*

### primary key

the one column that all tables include is an “ID” column,
which gives the unique row numbers,
and is called the record’s “primary key”.

### link tables & foreign key

can “link” tables together by making one of the columns in one table point to the ID of another table,
for instance a row in the “posts” table might include the author’s ID under the column called “user_id”.
Because the “posts” table has the ID of another table in it, that column is called a “foreign key”.


### Schema

The setup information for your database is stored in a special file called the “Schema”, and this is updated whenever you make changes to the structure of your database.

### index

index a column for faster searching later with CREATE INDEX.
Create indexes, which basically do all the hard work of sorting your table ahead of time, for columns that you’ll likely be using to search on later (like username)…
it will make your database much faster.

### sql "likes"

SQL likes semicolons at the end of lines
and using single quotes (‘) instead of double quotes(“).

### SQL CRUD statements

Every CRUDdy command in SQL contains a few parts – the action (“statement”), the table it should run on, and the conditions (“clauses”). If you just do an action on a table without specifying conditions, it will apply to the whole database and you’ll probably break something.

### sql destroy (cruD)

For “Destroy” queries, the classic mistake is typing DELETE FROM users without a WHERE clause, which removes all your users from the table. You probably needed to delete just one user, who you would specify based on some (hopefully unique) attribute like “name” or “id” as part of your condition clause, e.g. DELETE FROM users WHERE users.id = 1. You can do all kinds of common sense things like using >, <, <= etc. comparison operators to specify groups of rows to run commands on or logical operators like AND, OR, NOT etc to chain multiple clauses together, e.g. DELETE FROM users WHERE id > 12 AND name = 'foo'.


### sql create (Crud)

“Create” queries use INSERT INTO and you’ll need to specify which columns to insert stuff into and then which values to put in those columns, which looks something like INSERT INTO users (name, email) VALUES ('foobar','foo@bar.com');. This is one of the few queries that you don’t need to be careful about which rows you’ve selected since you’re actually just adding new ones into the table.

### sql update (crUd)

“Update” queries use UPDATE and you’ll need to tell it what data to SET (using key=”value” pairs) and which rows to do those updates for. Be careful because if your WHERE clause finds multiple rows (e.g. if you’ve searched based on a common first name), they’ll all get updated. A standard query for updating a user’s email may look something like the following (though in the real world you’d search on ID because it’s always unique):

```ruby
  UPDATE users
  SET name='barfoo', email='bar@foo.com'
  WHERE email='foo@bar.com';
  ```

  ### sql read (cRud)

“Read” queries, which use SELECT, are the most common, e.g. SELECT * FROM users WHERE created_at < '2013-12-11 15:35:59 -0800'. The * you see just says “all the columns”. Specify a column using both the table name and the column name. You can get away with just the column name for simple queries but as soon as there are more than one table involved, SQL will yell at you so just always specify the table name: SELECT users.id, users.name FROM users.

A close cousin of SELECT, for if you only want unique values of a column, is SELECT DISTINCT. Say you want a list of all the different names of your users without any duplicates… try SELECT DISTINCT users.name FROM users.