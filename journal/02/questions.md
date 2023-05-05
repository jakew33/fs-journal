# Intro to JavaScript

1.  Which keywords are used to declare a variable in JavaScript?

    > var, let, and const

2.  What is the definition of a function?

    > A function is a subprogramm designed to perform a specific task.

3.  What are the `SOLID` principles?

    > Single Responsibility a class should be having one and only one responsibility
    > Open / Closed classes should be open for extension but closed for modification
    > Liskov Substitution parent classes should be easily substituted with their child classes without blowing up the application
    > Interface Segregation many client specific interfaces are better than one general interface
    > Dependency Inversion classes should depend on abstraction but not on concretion

4.  Given this array: How could you remove the `pineapple`?

    ```js
    let fruit = ["apple", "banana", "pineapple", "orange", "strawberry"];
    ```

    > By using splice()

5.  Given these two objects: How could you add each to the others friends arrays?

    ```js
    let you = {
      name: "You",
      hair: true,
      friends: [],
    };
    let them = {
      name: "Them",
      hair: false,
      friends: [],
    };
    ```

    > you.friends.push(them);
    > them.friends.push(you);

6.  Give an example of a JavaScript `Conditional`:

    > if () {

    } else {

    }

7.  What is the main difference between `parameters` and `arguments`?

    > A parameter is a named variable passed into a function, an argument is a value passed as input to a function when invoked.

8.  Instead of writing everything to the console, what is a better way to debug your code?

    > Using the debugger built into Chrome

9.  What is the difference between a `primitive` value and a `reference` value?

    > A primative is data that is not an object, and has no methods or properties, if it's anything else than that it's a reference value.

10. Demonstrate a loop that prints the numbers between -100 and 100?

        > for (let i = -100; i <= 100; i++) {

    console.log(i);
    }
