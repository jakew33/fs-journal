# CSharp and SQL Fundamentals
01. What is the purpose of a `namespace`?

  > It organizes code into logical groups and prevents name collisions that can occur when your code base includes multiple libraries 

02. What is the difference between a `class` and an `interface`?

  > A class is a blueprint that is used to create objects that share the same properties and methods. An Interface is a group of related properties and methods that describe an object.

03. What is the method that returns an instance of a class, yet it has no return type?

  > Void

05. In the Car example what is the access modifier of the `Start()` method?

  ```c#
  abstract class Car
  {
    public string Start()
    {

      return "Vroooom";

    }
  }
  ```

  > public|

06. In the Car example what is `string` an indication of?

  > It indicates the return type of the method

07. In the Car example what is `abstract` preventing?

  > It prevents the inheritance of a class or class members that were previously marked virtual.  

08. In a SQL table, what is the difference between information in a row and information in a column?

  > Rows represent a single instance of data stored in a table, Columns represent specific value of a property of the data stored in a table

09. Demonstrate the necessary SQL for creating a table called `characters` with the values `name, age, description` as strings, and an `int` id.

  > CREATE TABLE characters(
    id INT NOT NULL
    name VARCHAR(255) NOT NULL
    age INT NOT NULL
    description VARCHAR(255) NOT NULL

  )

10. In SQL how can you query more than a single table? Provide an example.

  > SELECT movies, director FROM movies JOIN accounts director ON movie.directorId = director.id WHERE movie.id = movieId
