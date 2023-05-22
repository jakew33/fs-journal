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
