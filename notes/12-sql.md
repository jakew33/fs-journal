# SQL

in dbSetup.sql

CREATE TABLE penguins(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name TEXT NOT NULL,
  age INT DEFAULT 1,
  species TEXT
  wearingTuxedo BOOLEAN DEFAULT true
);

INSERT INTO penguins
(name, age, species)
VALUES
("Penny", 2, "Macaroni");

INSERT INTO penguins
(name, species)
VALUES
("Rocky", "Southern Rock Hopper");

INSERT INTO penguins
(name, species)
VALUES
("Stinky");

drop table and recreate it if you want to add more properties to your model

SELECT name, species FROM penguins WHERE id =1;



CREATE TABLE cars(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY
  make VARCHAR(100) NOT NULL
  model VARCHAR(100) NOT NULL
  year INTO NOT NULL DEFAULT 1990
  price DOUBLE NOT NULL DEFAULT 1.00
  color VARCHAR (100)
  description VARCHAR(500)
  updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP COMMENT 'Time Created',
  createdAt DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) default charset utf8 COMMENT '';

INSERT INTO cars
(make, model, year, price, color, description)
VALUES
("Fast", "Chevy", 2023, 20000, "Pearly", "kinda looks like a shitty cyber truck knockoff");

INSERT INTO cars
(make, model, year, price, color, description)
VALUES
("Mazda", "Miata", 2023, 34, "White", "It's a car");

SELECT * FROM cars ORDER BY price DESC;



Scale Grid Stuffs
---------------------

click databases/ new database

give database a name

go to Overview

look at the master connection

look at username and password, copy that shit

in the DB extension click the plus button, create a new connection, give it a name

host needs to be the master connection endpoint

username is sgroot
paste in admin password

fill out the name of the database/ whatever you named your database is what the name needs to be

click save, then connect

in appsettings.Development.json

paste in connection string add a port and user id with a space in the middle



create a new model called Car.cs


public class Car
{
  public int id {get; set;}
  public string Make {get; set;}
  public string Model {get; set;}
  public int Year {get; set;}
  public double Price {get; set;}
  public string Color {get; set;}
  public string Description {get; set;}
}

Make a car Controller

CarsController
[ApiController]
[Route("api/cars")]
public class CarsController : Controller Base
{

}


create a CarsService
----------------------------------

namespace sharpList.Services;

public class CarsService
{
  private readonly CarsRepository _repo;
}


back in Controller add

private readonly CarsService _carsService;

go to StartUp and add services 

services.AddScoped<CarsRepository>();
services.AddScoped<CarsService>();


Your repository needs a database

in CarsRepository

public class CarsRepository
{
  private readonly
}

in cars Controller

public ActionResult<List<Car>> GetAllCars(){
  try
  {
    List<Car> cars = _carsService>
  }
    catch (exception e)
  {

  }
}

in CarsService 

internal List<Car> GetAllCars()
{

}

in CarsRepository

internal List<Car> GetAllCars()
{
  string sql = "SELECT * FROM cars;";
  List<Car> cars = _db.Query<Car>(sql).ToList();
  return cars;
}


In CarsController

[HttpGet("{carId}")]
public ActionResult<Car> GetById()
{
  try
  {
    Car car = _repo/GetById(carId);
    if(car == null) throw Exception($"No car at {carId}")
    return car;
  }
}


in carsRepositorty

{
  <!-- string sql = $"SELECT * FROM cars WHERE id = {carId}"; -->
  string sql = "SELECT * FROM cars WHERE id = @carId;";
  Car car = _db.Query<Car>(sql, new { carId }).FirstOrDefault();
  return car;
}

C# Day3/SQL Day2
---------------------

in dbSetup.sql

create a table

CREATE TABLE albums(
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  category VARCHAR(255) NOT NULL DEFAULT "misc",
  coverImg VARCHAR(255) NOT NULL,
  archived BOOLEAN NOT NULL DEFAULT false,
  creatorId VARCHAR(255) NOT NULL,

  FOREIGN KEY (creatorID) REFERENCES accounts(id) ON DELETE CASCADE
) default charset utf8 COMMENT '';

INSERT INTO albums
(title, category, coverImg, archived, creatorId)
("Retro Pugs", "pugs", "*insert img url here*", false '*creator id goes here*');

DELETE FROM albums WHERE id = 1;

DELETE FROM accounts WHERE id = '*creator id goes here*'

SELECT 
title, 
name 
FROM albums 
JOIN accounts ON albums.creatorId = accounts.id;

creating an album

Crete a model
-------------

public class Album
{
  public int Id { get; set; }
  public string Title { get; set; }
  public string Category { get; set; }
  public bool Archived { get; set; }
  public string coverImg { get; set; }
  public string CreatorId { get; set; }
  public Account Creator{ get; set; }
}

Create Repository
Create Service
Create Controller 
Add Services to Startup.cs

in controller, write out the post function
bring in private readonly Auth0Provider _auth;

[HttpPost]
[Authorize] *This can also just be put on the controller if you want authorization to access everything*

public async Task <ActionResult<Album>> CreateAlbum([FromBody] Album albumData)
{
  try
  {
    Account userInfo = await _auth.GetUserInfoAsync<Account>(HttpContext);
    albumData.CreatorId = userInfo.Id

    Album album = _albumsService.CreateAlbum(albumData)
    return Ok(album);
  }
  catch (exception e)
  {
    return BadRequest(e.message)
  }
}

in services 

Album album = _repo.CreateAlbum(albumData);

in repo

string sql = @"
INSERT INTO albums
(title, category, coverImg, creatorId, archived)
VALUES
(@title, @category, @coverImg, @archived, @creatorId);

SELECT
  alb.* 
  FROM albums alb 
  JOIN accounts creator ON alb.creatorId = creator.id
  WHERE id = LAST_INSERT_ID();
";

Album album = _db.Query<Album, Account, Album>(sql, (album, account) =>
{
  album.Creator = creator;
  return album;
 
 }, albumData).FirstOrDefault();
 return album;

 in the controller

 [HttpGet]
 public ActionResult<List<Album>> GetAllAlbums(){
  try
  {

  }
  List<Album> albums = _albumsService.GetAllAlbums();
  {

  }
 }

 in AlbumsService

List<Album> albums = _albumsService.GetAllAlbums()
{
  string sql = @"
  SELECT
  alb.*,
  creator.*
  FROM albums alb 
  JOIN accounts creator ON alb.creatorId = creator.id;
  ";
  LIST<Album> albums = _db.Query<Album, Account, Album>(sql, (album, creator)=>(
    album.creator = creator;
    return album;
  )).ToList();
  return albums;
}

back in controller

[HttpGet{"(albumId)"}]
{
  try
  {

  }
  
  {

  }
}

In Services

{
  Album album = _repo.GetAlbumById(albumId)
  if(album == null) throw new Exception new Exception
}

internal Album GetById(int albumId)
{
  string sql =@"
  SELECT
  alb.*,
  creator.*!SECTIONFROM album alb
  JOIN accounts creator ON alb.creatorId = creatorId
  "WHERE alb.id = @albumId;
  ";

  Album album = _db.Query.<Album, Account, Album>(sql, (album, creator) =>
  {
    album.Creator = creator;
    return album;
  }, new { albumId }).FirstOrDefault();
  return album;
}

in Controller

[HttpDelete("albumId")]
[Authorize]


postItSharp pt.2
----------------

CREATE TABLE IF NOT EXISTS pictures(
  id INT NOT NULL AUTHO_INCREMENT PRIMARY KEY,
  imgUrl VARCHAR(255) NOT NULL,
  creatorId VARCHAR(255) NOT NULL,
  albumId INT NOT NULL,

  FOREIGN KEY (creatorID) REFERENCES accounts(id) ON DELETE CASCADE
  FOREIGN KEY (albumId) REFERENCES Albums(id) ON DELETE CASCADE
) default charset utf8 COMMENT '';


create a model

namespace postItSharp.Models;

public class Picture
{
  public int Id { get; set; }
  public string ImgUrl { get; set; }
  public string CreatorId { get; set; }
  public string AlbumId { get; set; }
  public Account Creator { get; set; }
}

Start making PicturesRepository

namespace postItSharp.Repositories;

public class PicturesRepositories
{
  private readonly IDbConnection _db;


}

Go make the service

Start making Pictures Service

namespace postItSharp.Services;

public class PicturesService
{
  private readonly PicturesRepository _repo;

  public PicturesService(PicturesRepository repo)
  {
    _repo = repo;
  }
}

Make A controller

{
  private readonly PicturesSeervice _picturesService;

  public PicturesController(PicturesService picturesService)
  {
    _picturesService = picturesService;
  }

  [HttpPost]
  [Authorize]

  public async <ActionResult<Picture>> CreatePicture([FromBody] Picture pictureData) ---> *this is like the req data*

{
  try
  {
    Account userInfo = await _auth0.GetUserInfoAsync<Account>(HttpContext);
    PictureData.CreatorId = userInfo.Id;
    Picture newPicture = _picturesService.CreatePicture(pictureData);
    return Ok(newPicture)
  }
  catch (Exception e)
  {
     return BadRequest(e.message);
  }
}
}

go back to service

internal Picture CreatePicture(Picture pictureData)
{
  Picture newPicture = _repo.CreatePicture(pictureData);
   return _repo.CreatePicture(pictureData);
   <!-- return _repo.CreatePicture(pictureData); --> *this is an optional way to do the two lines above*
}

in the repo

{
  string sql =@"
  INSERT INTO pictures
  (imgUrl, creatorId, albumId)
  VALUES
  (@imgUrl, @creatorId, @albumId);

  SELECT
  pic.*, *everything from the pictures table*
  act.* *everything from the accounts table*
  FROM pictures pic
  JOIN accounts act ON act.id = pic.creatorId
  WHERE pic.id = LAST_INSERT_ID()
  ;";
  Pictrue picture = _db.Query<Picture, Account, Picture>(sql,(picture, creator) => *Order matters here.*
  {
    picture.Creator = creator;
    return picture;
  }, pictureData).FirstOrDefault();
  return picture;
}

Writing out a get request

in Albums Controller

[HttpGet("albumId/pictures")]
public ActionResult<LIST<Picture>> GetPicturesByAlbumId(int albumId)
  {
  try
  {
    List<Picture> pictures = _picturesService.GetPicturesByAlbumId(albumId);
    return Ok(pictures);
  }
  catch (Exception e)
  {
    return BadRequest(e.Message);
  }

}

in services

internal List<Picture> GetPictureByAlbumId(int albumId)
{
  List<Picture> pictures = _repo.GetPicturesByAlbumId(albumId)
  return pictures;
}

in repo

internal List<Picture> GetPictureByAlbumId(int albumId)
{
  string sql = @"
  SELECT
  pic.*,
  act.*
  FROM pictures pic
  JOIN accounts act ON act.id = pic.creatorId
  WHERE pic.albumId = @albumId
  ;";
  LIST<Picture>albumPictures = _db.Query<Picture, Account, Picture>(sql, (picture, account)=>
  {
    picture.Creator = account;
    return picture;
  }, new {albumId}).ToList();
  return albumPictures;
}

Hard Delete Pictures

in controller

[HttpDelete("{pictureId}")]
[Authorize]
public ActionResult<string> DeletePicture(int pictureId)
{
  try
  {
    Account userInfo = _auth0.GetUserInfoAsync<Account>(HttpContext);
    _picturesService.DeletePicture(pictureId)
    return Ok()
  }
  catch (Exception e)
  {

  }
}


internalPicture GetById(int pictureId)
{
  Picture picture = _repo.GetPicturesById(pictureId);
  if(picture == null) new Exception("Invalid Id");
  return picture;
}

In Service

internal void DeletePicture(int pictureId, string userInfo)
{
  Picture picture = GetById(pictureId);
  if(picture.CreatorId != userId) new Exception("Not yours, bud");
  _repo.DeletePicture(pictureId);
}


in repo

internal Picture GetById(int pictureId)
{
  string sql = @"
  SELECT
  pic.*
  act.*!SECTIONFROM pictures pic
  Join accounts act ON act.id = pic.creatorId
  WHERE pic.id = @pictureId
  ;";
  Picture picture = _db.Query<Picture>
}


in repo

internal int DeletePicture(int pictureId)
{
  string sql = @"
  DELETE FROM pictures 
  WHERE id = @pictureId
  LIMIT 1
  ;";
  int rows = _db.Execute(sql, new {pictureId});
  return rows;
}

in service layer

internal void DeletePicture(int pictureId, string userInfo)
{
  Picture picture = GetById(pictureId);
  if(picture.CreatorId != userId) new Exception("Not yours, bud");
  _repo.DeletePicture(pictureId);
}
if(rows > 1) new Exception("Whoops");

Many to many relationships
-------------------------------

Start by making a new table for collaborators

CREATE TABLE IF NOT EXISTS collaborators(

albumId VARCHAR(255)
id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
creatorId INT NOT NULL,
accoountId VARCHAR(255) NOT NULL,
FOREIGN KEY (albumId) REFERENCES album(id) ON DELETE CASCADE,
FOREIGN KEY (accountId) REFERNECES accounts(id) ON DELETE CASCADE
) default charset utf8 COMMENT '';


INSERT INTO collaborators
(accountId, albumId)
VALUES ('*Id goes here*',23);

SELECT
collab.*,
act.*,
alb.*
FROM collaborators collab
JOIN accoints act On act.id = collab.accountsId
JOIN albums alb ON alb.id = collab.albumId;


go make a model

Collaborator.cs

namespace postItSharp.Models;

public class Collaborator
{
  public int Id { get; set; }
  public string AccountId { get; set; }
  public int AlbumId { get; set; }
}

public class CollaboratorAccount : Account  *Throw this in the account model*
{
  public int CollaborationId { get; set; }
}

public class CollaboratorAlbum : Album *throw this in the album model*
{
  public int CollaborationId { get; set; }
}


Make A Model
Make A Repo
Make A Service
Make A Controller

*Http Context is the request. the incoming thing that the client sent you*




