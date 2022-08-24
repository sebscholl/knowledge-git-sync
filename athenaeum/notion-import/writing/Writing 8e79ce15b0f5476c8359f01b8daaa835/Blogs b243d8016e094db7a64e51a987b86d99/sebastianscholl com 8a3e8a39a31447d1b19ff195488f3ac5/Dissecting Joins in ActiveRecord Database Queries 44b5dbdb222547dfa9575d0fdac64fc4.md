# Dissecting Joins in ActiveRecord Database Queries

Created: August 25, 2021 12:07 PM
Location: New York City, United State of America
Original Publish Date: March 20, 2016
Tags: Tech & Code

As databases grow, efficient querying becomes paramount. It’s easy to be sloppy in the beginning while racing to make something “work”. In the spirit of red, green, refactor though, we must revisit our methods and attempt at working off the fat.

Working with Rails allows us to conveniently communicate with our database. So convenient that it’s easy to develop some poor habits during development. How so? Let’s say we’re making a program to keep track of a school’s students. We’ve made a table in the database titled *students*. To return query all our *students*, all we need to write out is `Student.all`.

Rails is built on top of ActiveRecord, and ActiveRecord is the underlying workhorse whose methods we mostly rely on for communicating with our database. By writing out `Student.all`, it generated and executed the SQL statement `SELECT "students".* FROM "students”`, returning to us an array of all our student as objects.

Great. Now what if I want to find all the students named *John*? It’s still straight forward. Write out `Student.where(name: 'John')` and ActiveRecord will put together and execute the following SQL statement `SELECT "students".* FROM "students" WHERE "students"."name" = ?  [["name", "John"]]`, returning to us an array of all our students as objects whose name attribute is equal to *John*.

So where’s the fat and bad habits coming into play? Let’s beef up our program by adding several models and relationships. The first being that we are now building a system to keep track of state school systems. Reference the model below to understand the relationships.

```ruby
class State < ActiveRecord::Base
  has_many :districts
  has many :schools, through: :districts
end
```

```ruby
class District < ActiveRecord::Base
  belongs_to :state
  has_many :schools
end
```

```ruby
class School < ActiveRecord::Base
  belongs_to :district
  has_many :students
  has_many :teachers
end
```

```ruby
class Student < ActiveRecord::Base
  belongs_to :school
end
```

Again, we want to find all the students named John within a specific state. Well, a state knows all its’ schools and each school knows all its’ students. If we write out `State.schools` we get all the schools, and then we can iterate over each school and gather its' students through `school.students`, and then iterate over each student to select only those students whose `student.name == “John”`.

The code would look something like this (I didn't run it to find out...), and it is about as awful to read as the sentence just written explaining how it works.

```ruby
State.schools.map do |school|
  school.students.select do |student|
    student.name == "John"
  end
end.flatten.compact
```

We'd be fine if states had five school and each school only around 200 students. The reason being that iterating over every single student within every single school within a state is not too taxing on our computer if there's only 1000 students. Obviously though, if there were 1,000,000 students or 10,000,000 students... that search might take awhile.

Instead of putting all that stress on our computer's memory and processor, we can instead refine our search methods as to give our database exact instructions as to what we're looking for. In the last example, our database first gave us a list of all the schools. Then we asked it to retrieve a list of all the school's students - one school at a time - and every time it returned a list of students, we had to go through that list ourselves to check whether or not the student's name was *John*. No fun for anyone!

![https://mynamessebastian.files.wordpress.com/2013/11/0a9a1784.jpg](https://mynamessebastian.files.wordpress.com/2013/11/0a9a1784.jpg)

It would be great if we could just tell our database something as simple as `State.students.where(name: "John")`. By using *Joins*, we can get pretty close.

Our tables track relationships in our models through [primary and foreign keys](https://msdn.microsoft.com/en-us/library/ms179610.aspx). So if a *student* belongs to a *school*, that student will hold the schools ID within its' row of data. If we made a new model named *Course*, it would probably have many *students*, and *students* would have many courses. Thus, a separate table called *student_courses* would be created to keep track of their *has-many to has-many* relationship by holding the ID from both in a single row.

What *Joins* allow us to do is tell the database to merge data from multiple tables. The reason they are called "Joins" is because of the way we specify where to merge the datasets. In our case, a school hold the primary key of its district, which holds the primary key of its state. Thus, `State.joins(:schools)` would return us a list of each school's state (not very useful...). However if we specify what we want to see using a .select() method as so `State.select("schools.name").joins(:schools)`,  we are now returned a list of all the schools - names - from our database.

So lets move a step further. We know that a student belongs to a school, so lets now join the *students* table. We can do this with the following syntax `State.select("states.id, schools.name").joins(:schools => :students)`, which generates and executes the SQL statement:

```sql
SELECT states.id, students.name 
	FROM "states" 
	INNER JOIN "districts" 
	ON "districts"."state_id" = "states"."id" 
	INNER JOIN "schools" 
	ON "schools"."district_id" = "districts"."id" 
	INNER JOIN "students" 
	ON "students"."school_id" = "schools"."id"
```

Take a moment to read the above SQL query carefully as to understand exactly how it's running. It's joining together each row from each table where the foreign keys/primary keys match. And from that newly formed row, we are specifying which columns we are interested in seeing. In the example above, we are returning all of our state's IDs and student's names - but once again, we only want to see the ones named John.

We can now take another step forward by using a `.where()` method, making our query `State.select("states.id, students.name").joins(:schools => :students).where("students.name = "John"")` and generating the following SQL statement:

```sql
SELECT states.id, students.name 
	FROM "states" 
	INNER JOIN "districts" 
	ON "districts"."state_id" = "states"."id" 
	INNER JOIN "schools" 
	ON "schools"."district_id" = "districts"."id" 
	INNER JOIN "students" 
	ON "students"."school_id" = "schools"."id" 
	WHERE (students.name = 'John')
```

We've come a long way from where we started! Using the query above, our database returned a list of all the students named John, starting at the *states* table. Pretty cool! There is only one little change that needs to be made - and that change is that we don't want ALL the students named John. Instead, we are looking for the students named John **within** a specific state. This can be achieved by simply adding a second condition to our .where() method, wrapping the whole thing up as so:

```ruby
State
	.select("states.id, students.name")
	.joins(:schools => :students)
	.where("students.name = 'John' AND states.id = 1")
```

```sql
SELECT states.id, students.name 
	FROM "states" 
	INNER JOIN "districts" 
	ON "districts"."state_id" = "states"."id" 
	INNER JOIN "schools" 
	ON "schools"."district_id" = "districts"."id" 
	INNER JOIN "students" 
	ON "students"."school_id" = "schools"."id" 
	WHERE (students.name = 'John' AND states.id = 1)
```

Here we are assuming that we know the states primary key and are throwing it in as an argument. By doing so...voilá! We were able to give our database a very specific set of instructions as to exactly what information we were looking for. In return - in one go - it was able to return to us the "list" - array of objects - we were looking for in one swoop.

![https://mynamessebastian.files.wordpress.com/2014/06/old-car.jpg](https://mynamessebastian.files.wordpress.com/2014/06/old-car.jpg)

## Practical Implementation:

Above's step by step explanation was to show how ActiveRecord builds the SQL query. However now that we have it, how do we use it? We can't expect some to go in and edit out *John* with the name they are looking for, as well as to look up and input a states primary key. So instead, lets wrap it up as an instance method that accepts an argument for the name.

Here is our *State* model. Notice how it's updated it with a new method - *find_students_by_name(student_name)*:

```ruby
class State < ActiveRecord::Base
  has_many :districts
  has many :schools, through: :districts

  def find_students_by_name(student_name)
    State.select("students.name")
			.joins(:schools => :students)
			.where("students.name = ? AND states.id = ?", student_name, self.id)
  end
end
```

Now any instance of *State* can easily find all its' students by name! Meaning that if `new_york` were a variable for an instance of *State*, we could simply write out `new_york.find_students_by_name("John")` and be returned the students we were looking for.