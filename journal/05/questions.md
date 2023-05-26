# Intro to Server side concerns with JavaScript
01. What do the letters of the acronym `CRUD` stand for?

  > Create, Read, Updated, Delete

02. Each action that `CRUD` represents maps to an HTTP request. What HTTP request does each `CRUD` action correspond to?

  > Create/Post, Read/Get, Update/Put, Delete/Delete

03. What does `ORM` stand for? Which `ORM` do we use when interacting with MongoDB

  > Object Relational Mapping

04. Which two `HTTP` request types include a body?

  > Post, Put

05. In a/an _______ coding model, when you call a function, it returns only when the action has finished and stops your program for the time the action takes. Likewise in a/an _______ coding model, multiple things are allowed to happen at one time. When you perform an action, your program continues to run.  Fill in the blanks.

  > Synchronous, Asynchronous 

06. What are the three types of data relationships? Provide an example of each.

  > One-to-one, one-to-many, many-to-many

  1:1/ An author has a single address, and the address contains a single author
  1:N/ A post may have many comments, but a comment is only related to a single post
  N:M/ A book written by many authors. One of those authors may have wrote many books

07. What is middleware?

  > a function that has access to both the request object, and the response object

08. The ______ pipeline delivers information from the client while the ______ pipeline returns it. Fill in the blanks. 

  > Request, Response

09. Demonstrate the pattern that is used to include a request query with the client's `HTTP` request providing the property `tag` and the value `winter`.

  > | ANSWER HERE |

10. What is a ***virtual property***?

  > A property not stored in MongoDB
