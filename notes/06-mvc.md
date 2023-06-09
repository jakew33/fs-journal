# MVC

use express-vue

set up your env

start client, spin your server

get your bearer token

make sure auth0 is connected, make sure Back-end is connected

1. 

make a model.js

Album.js --->

export { Schema } from "mongoose"
const ObjectId = Schema.Types.ObjectId

export const AlbumSchema = new Schema(
{
 title: {type: String, required: true, maxlength: 25, min, minlength: 3},
 category {type: String, required: true, enum: [ 'cats', 'pugs', 'games', 'books', 'aesthetics, 'tattoos', 'technology']
}, 
coverImg: {type:String, required: true, maxlength: 300, default: 'https://'}
archived: { type: String, required: true, maxlength: 300, default: 'https//'}
creatorId: {type: Schema.Types.ObjectId, required: true, ref: 'Account'}
}, {timeStamps: true, toJSON: { virtuals: true} }
)

AlbumSchema.virtual('creator', {
  localField: 'creatorId',
  foreignField: '_id',
  ref: 'Account',
  justOne: true
})

Register the model in the DBContext

Albums = mongoose.model('Albums', AlbumSchema)

2. 

Create an Albums Controller, Albums Service

class AlbumsService{

}

export const albumsService = new AlbumsService()

export class AlbumsController extends BaseController{
  constructor() {
    super('api/albumss')
    this.router

  }
}

3. 

Start testing in PostMan

{{endpoint}}/api/albums

setup bearer token

in auth  Initial Value, Other, put in token

when testing, Posts have to work first. Test in the order that postMan has set up 


4.

in controller

export class AlbumsController extends BaseController{
  constructor() {
    super('api/albumss')
    this.router
    .use(Auth0Provider.getAuthorizedUserInfo)
    .post('', this.create)

  }
   async create (req,res,next) {
      try {
        req.body.creatorId = req.userInfo.id
      const albume = await albumsService.create(req.body)
        return res.send(album)
      } catch (error) {
        next(error)
    }
   }
}

in albumsService 


 class AlbumsService{
 create(albumData) {
  const album = await dbContext.Albums.create(albumData)

 }
}

export const albumsService = new AlbumsService()     




export class AlbumsController extends BaseController{
  constructor() {
    super('api/albumss')
    this.router
    .use(Auth0Provider.getAuthorizedUserInfo)
    .post('', this.create)
    .get('', this.findAllAlbums)
    .get('/:id', this.findAlbumsById)

  }
   async create (req,res,next) {
      try {
        req.body.creatorId = req.userInfo.id
      const album = await albumsService.create(req.body)
        return res.send(album)
      } catch (error) {
        next(error)
    }
     async findAllAlbums(req,res,next)
     try
     const albums = await albumsService.findAllAlbums(
      return res.data.send(albums)
      catch(error) {
        next(error)
      }
     )


      in service 

     async findAlbumById(albumId) {
      const albums = await dbContext.Albums.findById
      }
     }
   }


everytime you pull info from the database, you have to populate it



client side
getting albums drawing to the page


1. 
  set up your env in client side

  in server side, create the env

  in the home page client side 

  create an Album.js model

  export class Album{
    constructor(data) {
      super(data)
      this.id = data.id
      this.title = data.title
      this.category = data.category
      this.coverImg = data.coverImg
      this.archived = data.archived
      this.creatorId = data.creatorId
      this.creator = new Profile(data.creator)
    }
  }


in Account.js v

  export class Profile{

    constructor(data) {
      this.name = data.name
      this.picture = data.picture
      this.id = data.id
    }
  }

  Make Picture.js model

  export class Picture{
    constructor(data){
      this.id = data.id
      this.imgUrl = data.imgUrl
      this.creatorId = data.creatorId
      this.albumId = data.albumId
      this.creator = new Profile(data.creator)
    }
  }





  in Services create AlbumsService.js

  class AlbumsService{

  }

  export const albumsService = new AlbumsService()



  in the HomePage.vue

  async getAlbums(){
    try {
      await albumsService.getAlbums()
    } catch (error) {
      Pop.error(error.message)
    }
  }

  onMounted(() =>){
    getAlbums()

    return{}
  }

  in AlbumsService 

  async getAlbums(){
    const res = await api.get('api/albums')
    logger.log('[Getting Albums]', res.data)

  }

  save data to the appsatae

  import Albums model
  albums: []

    async getAlbums(){
    const res = await api.get('api/albums')
    logger.log('[Getting Albums]', res.data)
    AppState.albums = res.data.map(a => new Album(a))
    logger.log(AppState)
  }


    async getAlbums(){
    try {
      await albumsService.getAlbums()
    } catch (error) {
      Pop.error(error.message)
    }
  }

  onMounted(() =>){
    getAlbums()

    return{
      albums: computed(()=>AppState.albums)
    }
  }


create a template to display the data

throw template into HomePage.vue

<AlbumCard /> ---> displays the content of the AlbumCard


in the AlbumCard

export default 
props: [
album: { type: Album , required: true }
]

in HomePage 

<AlbumCard :album="a" />


in App.vue

<main class ="background-image"

.background-img{
  background-image: url('./assets/img/backgroundImg.png')
}


in router.js
set up a path for albums

path: '/about',
name 'About',


make AlbumDetailsPage.vue

in AlbumCard
set up a router-link


ALbumsDetailPage

async function getAlbumsById() {
  try {
    logger.log('getting albumsbyid')
  } catch (error) {
    logger.error(error)
    Pop.toast
  }
}

onMounted (()=> {

})


grab id from url

class PicturesService {
  async getPicturesByAlbumId(albumId) {
    const res = await api.get(``)
  }
}

import pictures into AppState

pictures: []

create Modal.vue

<slot></slot>
