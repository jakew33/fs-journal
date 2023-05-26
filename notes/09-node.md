# Node

npm i -g bcw to update to 3.3.16

bcw create
chose node-server-auth0


client folder - only has Index.html. It's where you build your client to

server - has package.json/ looks like a js object

our template is written around express. = core library that were using while running backend servers

helmet = keeps server secure

mongoose is what we use to talk about our data base

socket.io 


you have to be in the directory where you have a package.json, then run npm i in console. it reads package.json file, then installs all the things

node modules folder is where everything is stored

don't mess with any package. files

ignore node modules in c spell: ignore paths, under files exclude add the files you dont want to see

npm init - f adds package.json file

inside file is scripts name is "start" : "node index.js"


in .env


in server open main.js

in values controller 
 constructor() {
  super('api/values')

  this.router
  .get('', this.getAll)
 }


 everytime you make a change to your controller, re-spin your server



 export class TigersController extends BaseController {
  constructor() {
    super('api/tigers')

    this.router
    .get('')   
    <!-- if you dont modify the url you can put it in as an empty dtring -->
  }

  async getTigers(req, res, next){
    try {
      console.log (wut is the req, req)
      console.log(wut is the res, res)
    } catch (error) {
      next(error)
    }
  }
 }


in database folder 

export const Fakedb = {
  tigers: [
    {name: 'tony', picture: '' id: '11237b'}
    {name: 'harry', picture: '' id: '11237b'}
  ],

  characters [

  ]
}


to post data add .post to this.router

gets and deletes dont have bodies, posts and puts do

deleteTigerById(tigerId) pass in a param "tigerId"




NODE DAY 2 GREGS LIST NODE SERVER
---------------------------------

bcw create chose express-mvc

open workplace file

step 1 - add env variables from sandbox notepd file

add 3000 to PORT if it doesn't default

then add the new env file into notepad file to paste in for future projects

open client folder locate env.js - paste in the same variables as before

you want to be in the client to run console

make a new account

use the  access token to test your server


make cars model

Car.js

(Schema is same as a model)

car model v

import mongoose from "mongoose";
const Scehma = mongoose.Schema

export const CarSchema = new Schema(

    model: { type:String,, required: true, minLength: 3 },
    make: { type: String, required: true },
    year: { type: Number, required: true },
    leaksOil: { type: Boolean, default:false },
    engineType: { type:String, enum:['8 Cylinder', 'Six Cylinder', 'EV'], required: true }
    description: { type: String, required: true, maxLength: 500 
    },
    { timeStamps: true }
)


    step 2.

    in DbContext.js, register model under class DbContext

    Cars = mongoose.model('Car', CarSchema)

    step 3.
    
     make cars service

     step 4. 
     make Cars Controller

     export class CarsController extends BaseController{
      constructor() {
        super('api/cars') 
        this.router
        .get('', this.getCars)
      }

      getCars(request, response, next) {
        try {
        const cars = await carsService.getCars()
          return response.send()
        } catch (error) {
            next(error)
        }
      }
     }

     class CarsService {
      async getCars() {
        const cars = await dbContext.Cars.find()
        return cars
      }

     }

     in postman make a new collection/ Gregslist make new folder 'Cars'

     in cars controller add

     .use(Auth0Provider.getAuthorizedUserInfo)
     .post('', this.createCar)


in controller 

createCar(req, res, next) {
  try {
    const carData = req.body
    const newCar = await carsService.createCar(carData)
    res.send(newCar)
      res.send('create car successful')
  } catch (error)
    next(error)
}


in cars service...

async createCar(carData) {
  const newCar = await dbContext.Cars.creat(carData)
  return newCar
}




Week 5 Node- Day 3


express mvc

init an publish before writing code

run ls in cmd console to see files

parent collection = School

school schema

import mongooses from 'mongoose'

const Schema  = mongoose.Schema

export const SchoolSchema = new Schema ({
  name: {type:String, requires: true, maxLength: 25},
  location {type: string, required: true},
  isPrivate {type: Boolean, default: false},
  mascot {type: String, required: true},
  type: {type: String, enum:['elementary', 'highschool', 'middle school', 'alternative', 'clown']}
})

register schema in Database

Schools = mongoose.model('School', SchoolSchema)

when doing create methodes switch to raw in postman

+0




how to add a collaborator in github --->
in settings/access 
manage access/ add teams


virtuals = 
 can be an account, or  creator
 local field = id that we put into the schema that contains the reference
 local field will match

 foreign field = mongo db ID
 just one = only one person can create the object
 ref = references the account 


 



