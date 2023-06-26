# CSharp

decimal is the largest datatype.

Console.WriteLine is the new console.log/logger.log

strings can only be created with ""
if you want a single character use ''

string interpolation is now $"now you can sya {cool} with a {letter}";

bool tru = true;
bool no = false;

bool nothing = null;
int nada = null;
string zero = null;

add a question mark on the data typ to make things null

if(nothing == null){
Console.WriteLine(nothing);
}

if(x == 6)
{
  Consol.WriteLine("no truthy falsey");
}

'undefined' does not exist in C#

building an object. objects in c# are called dictionaries

Dictionaries have 2 data types. the data type of the key the data type of the value

Dictionary<string, string> dict = new Dictionary<string, string> { };
dict.Add("one", "anotha one");
dict.Add("two", "anotha one");
dict.Remove("two");

class Cat{

  int age;
  string name;

  public Cat (int age, string name) 
  {
    this.name = name;
    this.age = age;
  }
}

arrays have fixed lengths that cannot be increased or decreased so they are hard to work with

list =

List <int> numbers = new List <int>{} ...You can create indexes in these curly brackets like this {0,9,8,7,6}
numbers.Add(1)
numbers.Add(2)
numbers.Add(3)
numbers.Add(4)
numbers.Add(5)
numbers.Remove(3)
List<int> lowNumbers = numbers.FindAll(n => n <= 3);  to filter
int five = numbers.Find(n => n == 5);

numbers.forEach(n =>
Console.WriteLine(n)
)

lists do not have lengths, they have counts

var does exist in C#

do not create variables

bcw create
use,
dotnet-auth
do not name anything with a hyphen in it
namespaces cannot have hyphens in them. use underscores
dotnet restore is the equivalent of npm i

progrma.cs is the entry point of the project
csproj is like the project JSON file

comment out

do not click the add configuration button


base language support for C#/ C#
c# Extensions C# IDE Extensions for VSCode
MySQL

in models

namespace catRoundUp.Models;

public class Account
{
  public string Id { get; set; }
  public string Name { get; set; }
  public string Email { get; set; }
  public string Picture { get; set; }
}

Makin a model in C#!SECTION
to be able to import and export files you have to define you classes in namespaces

namespace carRoundUP.Models;

 or use prop and it'll fill it out for you

public class Cat  (go here and hit control period and it will write out your constructor for you)
{
  public string name {get; set;}
  public int Age  Age { get; set;}
  public string Color  Age { get; set;}
  public bool LongHair { get; set;}
  public bool Penned { get; set;}
}

making a controller in C#
--------------------------
namespace catRoundUp.Controllers;

[ApiController]
[Route("api/cats")]
public class catsController : ControllerBase
{

[HttpGet]
public string Test()
  {
    return "hey";
  }

}


[HttpGet]
public ActionResult<string> Test()
  {
    try
    {
    return OK("hey")
    }
    catch (System.Exception)
    {
    return BadRequest("I Can't Do That")
    }
  }


  [HttpGet]
public ActionResult<string> Test()
  {
    try
    {
    return OK("hey")
    }
    catch (System.Exception error)
    {
    return BadRequest("I Can't Do That" + error.Message);
    }
  }

ActionResult is a base class that contains info tht sends back network requests

Ok, and BadRequest are children of ActionResult

the end of a statement needs a ;
expressions need to be ended in ;


  [HttpGet("test")]
public ActionResult<string> Test()
  {
    try
    {
    return OK("hey")
    }
    catch (System.Exception error)
    {
    return BadRequest("I Can't Do That" + error.Message);
    }
  }


  [HttpGet("test")]
public ActionResult<string> Test()
  {
    try
    {
    return OK("hey")
    }
    catch (System.Exception error)
    {
    return BadRequest("I Can't Do That" + error.Message);
    }

------------------------

    [HttpGet]
    public ActionResult<List<Cat>> GetAllCats(){
      try
      {
        List<Cat> cats = ??go to my service and get the cats
        return Ok(cats); ...(this is a scoped variable, they can be lowercased)
      }
      catch(Exceptions e)
      {
        return BadRequest(e.Message);
      }
    }
  }

  using System;
  using System.Collections.Generic;
  using System.Linq;
  using System.Threading.Tasks; ...(this is how you use imports in C#)

  namespace catRoundUp.Services

  public class CatsSevice
  {
    public List<Cat> GetAllCats()
    {
      List<Cat> cats = catsService.GetAllCats();
      return cats;
    }
  }

  in catsController

  private readonly CatsService catsService;

  in CatsRepo
  \public class CatsRepository
  {
    private List <Cat> dbCats = new List<Cat>{};

    //Fake DB Stuff v

    public CatsRepository()
    {
      this.dbCats = new List <Cat>{}
      dbCats.Add(new Cat("Murdoc", 31, "black", true, false));
      dbCats.Add(new Cat("Pretty Kitty", 5, "tabby", true, false));
      dbCats.Add(new Cat("Sylvester", 5, "black & white", false, false));
    }
  }

  internal List<Cat> GetAllCats()
  {
    return dbCats;
  }

  

