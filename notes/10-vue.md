# Vue

bcw create/ vue-starter

components are chunks of reusable code

account: computed(() => AppState.account)

data binding = v-bind or : (says add the disabled attribute if there is no account logged in)

in env.js paste the blue text things into the corresponding exports

computeds at the bottom methods at the top (order of things)

method/
 incrementNumber() {
  this.number++
}

@click = "incrementNumber" in HTML

always use logger instead of console log when using Vue

 incrementNumber() {
logger.log('increasing the number')
  this.number++
},

you don't have to invoke you functions but you can


 incrementNumber() {
logger.log('increasing the number')
  AppState.number++
},



in env.js change out what you want the base url to be

onMOunted = runs whatever blok of code is inside of it as soon as the page/components
mounts or renders. this is similar to calling a function/method in the constructor of a controller

onMounted(() =>) {

getCars()
}


in carsService:

class CarsService {

async getCars() {
  const res = await api.get('api/cars')
  logger.log('gettingCars' res.data)

}


  export class carsService = new CarsService()
}

in AppState.js cars: []

Car.js

export class Car{

constructor(data) {
  this.id = data.id
  this.make = data.make
  this.model = data.model
  this. imgUrl = data.imgUrl
  this.year = data.year
  this.price = data.price
  this.description = data.description
  this.enginType= data.engineType
  this.createdAt = new Data(data.createdAt)
  this.creatorId = data.creatorId
  this.creator = data.creator
  }
}

in account.js...

export class Profile {
  constructor(data) {
    this.id = data.id
    this.email = data.email
    this.name = data.name
    this.picture = data.picture
  }
}

(this is called inheritance)

export class Account  extends Profile{

  constructor(data) {
    super(data)
    this.email = data.email
  }
}

export class Car{

constructor(data) {
  this.id = data.id
  this.make = data.make
  this.model = data.model
  this. imgUrl = data.imgUrl
  this.year = data.year
  this.price = data.price
  this.description = data.description
  this.enginType= data.engineType
  this.createdAt = new Data(data.createdAt)
  this.creatorId = data.creatorId
  this.creator = new Profile (data.creator)
  }
}

import Car model into APpState


in CarsService 

async getCars() {
  const res = await api.get('api/cars')
  logger.log('gettingCars' res.data)
  AppState.cars = res.data.map(c => new Car(c))

}


in cars page in the return...

cars: computed(() => AppState.cars)



App.vue is like the HTML

make a new component...

CarCard

bring HTML template into this

in CarsPage bring in the CarCard Component 


use props when you want to draw something many times

Vue day 2---

---------------------------------------------------- 
vue-starter

1. 
    In AxiosService, setup a new axios instance

    export const movieApi = Axios.create({
      baseURL: 'https:/',
      timeout 8000,
      params:
      {
        (additional params here...)
        api_key: 'key goes here'
        includes_adult: false,
        certification_country: 'US',
        'certification-lte': 'PG-13',
        'certification-gte': 'G'
      }
    })


2. 
    Get data from API first before making the model
    in HomePage.vue in export default (await import('vue')) ({
      setup (){
    -------------------------------------------------
        async function getMovies() {
          try
          logger.log('')
          catch (error) {
            logger.error(error)
            pop.toast(error.message, 'error')
          }
        }

        onMounted(() => {
          getMovies()
        })
        return{}
      }
    })

3. 
    Create MoviesService.js

    class MoviesService

    export class moviesService = new MoviesService

4.  
    in HomePage

    async function getMovies() {
      try
      await moviesService.getMovies()
      logger.log('')
      catch (error) {
        logger.error(error)
        pop.toast(error.message, 'error')
      }
    }

    onMounted(() => {
      getMovies()
    })
    return{}

5. 
    in MoviesService

      class MoviesService

      async getMovies( {
        const res = await movieApi.get('discover/movie')
        logger.log('getting movies', res.data)
      })

  export class moviesService = new MoviesService

6. 
    make Movie.js model

    export class Movie{
      constructor(data) {
         this.id = data.id
         this.backdropImg = `https://image...${data.backdrop_path}`  <--- Image Path
         this.posterImg 'https...' + data.poster_path
         this.title = data.original_title
         this.description = data.overview
         this.releaseDate = data.release_Date
         this.average = data.vote_average

      }
    }

7. 
    in movies service 

      async getMovies( {
        const res = await movieApi.get('discover/movie')
        logger.log('getting movies', res.data)
        AppState.movies = res.data.map(m=>new Movie (m))
        logger.log()
      })

  export class moviesService = new MoviesService


8. 
    in AppState

    import Movie model

    moveis: []
    

9. 
    in movies service 

    async getMovies( {
      const res = await movieApi.get('discover/movie')
      logger.log('getting movies', res.data)
      AppState.movies = res.data.results.map(m=>new Movie (m))
      logger.log(AppState.Movies, 'appState movies')
    })

  export class moviesService = new MoviesService



10. 
    in movies service, comment out console logs to avoid clutter

    async getMovies( {
      const res = await movieApi.get('discover/movie')
      AppState.movies = res.data.results.map(m=>new Movie (m))
    })

  export class moviesService = new MoviesService

11. 
    in HomePage

    async function getMovies() {
      try
      await moviesService.getMovies()
      logger.log('')
      catch (error) {
        logger.error(error)
        pop.toast(error.message, 'error')
      }
    }

    onMounted(() => {
      getMovies()
    })
    return{

      movies: computed(() => AppState.movies)
    }


12. 
    in the template tag in HomePage start making template to display everything
    


13. 
    make a MovieCard 

    import movie card into HomePage.vue

    in Movie Card

    props: (
        movieProp: { type:Movie, required: true }
    )

    in HomePage 
    <MovieCard :movieProp="m" />

    im movieCard

    :src "movieProp.posterImg" :alt= "movieProp.title">  ...add elvis operators (?) if you get errors

14. 
   in movie card

   bring in the router:

   <router-Link :to="{ name: 'MovieDetails' }"
   
   </router-Link>

15.   
    make moviesDetailsPage...
    setup with snippet we don't have

    in router.js

    path: '/movie:movieDetails',
    name: 'MovieDetails',
    component: loadPage('MoviesDetailPage')


16. 
   in movie card add params:{ movieId: movieProp.id }

17. 
    in movies details page...

    setup()
        const route = useRoute(),

        async function getMovieById() {
          try
          const movieId = route.params.movieId
          await moviesService.getMovieById(movieId)
          catch (error)
          logger.error(error)
          pop.toast(error.message, 'error')
        }
        onMounted(()=> {

        })


    return {};


18. in movies service

async getMoviesById( {
  const res = await movieApi.get(`movie/${movieId}`)
  logger.log('getting movie by id', res.data)
  AppState.activeMovie = new Movie(res.data) 
  logger.log('appState movie ')
})


19. 
  in appstate add activeMovie: null/ import model



20. 
  in MovieDetailsPage

        setup()
        const route = useRoute(),

        async function getMovieById() {
          try
          const movieId = route.params.movieId
          await moviesService.getMovieById(movieId)
          catch (error)
          logger.error(error)
          pop.toast(error.message, 'error')
        }
        onMounted(()=> {

        })


    return {

      movie: computed(() => AppState.activeMovie)
    };


21. 
  in moviesdetail page to set a background

  :style="{backgroundImage: `url(movie?.backdropImg)`}"


22. 
  make a search bar

  in HomePage style the search bar

23. 
  abstract searchbar and add it to it's own component

  create SearchBar.vue, inject search bar html

  @sumbit.prevent="searchMovie()"


  setup() {
    const searchTerm = ref('')
    return {
        searchTerm, 
      async searchMovie() {
        try
        logger.log
        catch (error) {
          logger.error(error)
          pop.toast(error.message, 'error')
        }
      }
    }


  }

  in input above imports add class="w-100 v-model="search" placeholder="Search..."

  make sure you import "ref"


24. 

  setup() {
    const search = ref('')
    return {
        searchTerm, 
      async searchMovie() {
        try
        const searchTerm = search.value
        logger.log(' searching movie', searchTerm)
        await moviesService.searchMovie(searchTerm)
        catch (error) {
          logger.error(error)
          pop.toast(error.message, 'error')
        }
      }
    }


  }

  in input above imports add class="w-100 v-model="searchTerm" placeholder="Search..."

  make sure you import "ref"


25. 
    in moviesService 
  async searchMovies(query) {
    const res = await movieApi.get('search/movie',{ 
      params: 
        query: searchTerm
        api_key: 'key goes here'
        includes_adult: false,
        certification_country: 'US',
        'certification-lte': 'PG-13',
        'certification-gte': 'G' 
        })
    logger.log('searching movies', res.data)
    appState.movies = res.data.results. map(m => new Movie(m))
  }

26. 
    in AppState 

    currentPage: null,

    totalPages: null

  27. 
  in moviesservice

 async getMovies
 AppState.totalPages
 AppState.
 AppStae.



 in HomePage 

 return {
  async changePage() {
    try
    if(pageChangeSwitch == 'next') {
    AppState.currentPage++
    }esle if (pageChangeSwitch ==)
    AppStateCurrentPage --
    logger.log
    logger.log
    await moviesService.changePage()
    catch(error)
    pop.toast(error.message "error")
  }
 }

 current page: computed(() => )
 totalPages: computed (()=> )
 movies: computed(() => AppState.movies)



28. 
 in movies service 

 changePage() {
  const res = await movieApi.get(`discover/movie?page=${appState.currentPage}`)
  logger.log('changing page', res.data )9999
  AppState.movies = res.data.results.map(m => new Movie(m))
  
 }

 in AppState

 query: null

  changePage() {
  const res = await movieApi.get(`discover/movie?page=${appState.currentPage}`)
  logger.log('changing page', res.data )
  AppState.movies = res.data.results.map(m => new Movie(m))
  
 }

under search movies in moviesService 

AppState.query = searchTerm

  changePage() {
    const query = AppState.query

    if(1query) {
  const res = await movieApi.get(`discover/movie?page=${appState.currentPage}`)

    }else {
      const res = await movieApi.get('search/movie')
      params:
      query: query, ....
    }
  logger.log('changing page', res.data )
  AppState.movies = res.data.results.map(m => new Movie(m))
  
 }

 you need to know pagenation for the checkpoint



 Vue Day 3
--------------------------------------------

setup your env.js


editing accounts --->

in the router look at the account route. it loads the account page

you can add:

this.bio = data.bip
this.coverImag = data.coverImg
this.resume = data.resume
this.socialPlatafrom = data.github

in account page 

raw data dump V
{{ account data }}

.account-page {
  background-image: v-bind(coverImg);

.account-picture{
  height: 100px;
  aspect-ratio: 1/1;
  object-fit: cover
  }
}


under account: computed(() => AppState.account),
coverImg: computed(() => `url(${AppState.account?.coverImg})`)


in template...

div class = "container_fluid"
div class = "row"
div class = "col-md-3"
div class = card
div class = card body
p class = text-center
img :src= "account.picture" :alt="account name"
p User: {{ account.name }}

to hide socialplatform

v-if='account.socialPlatform'

don't write forms inside of pages
keep pages around 100-150 lines of code


in account form

<form @submit.prevent="editedAccount">
<div>
<input class="form-control" placeholder="Name" type="text" required v-model="editable.name">
<input class="form-control" placeholder="Profile Picture" type="text" required v-model="editable.picture">
<input class="form-control" placeholder="cover Image" type="text" required v-model="editable.coverImg">
</div>


export default
setup(){
  const editable = ref({})

  watchEffect(() => {
    editable.value = { ...AppState.account }
  })

  

  return{
    editable,
    async handleSubmit() {
      try {
          accountService.editAccount(editable.value) <--- saves account changes
      }catch (error) {
        Pop.error(error, '[editing account]')
      }
    }
  }
}

in account service

async editAccount(fromData){
  const res = await api.put('/account', formData)
  AppState.account new Account(res.data)
}


export class Project {
  constructor(data){
    this.id = data.id
    this.title = data.title
    this.creator= data.creator
    this.creatorId = data.id
    this.id = data.id
    this.id = data.id
  }
}

class ProjectsService {
  async getProjects() {
    const res = await api.get('api/projects')
    logger.log(res.data)
    AppStae.projects = res.data.map(p => new Project(p))
  }

}
export const projectsService = new ProjectsService


in home page under setup()

async function getProjects
try {

}catch (error) {
  Pop.error(error, "getting projects")
}
onMounted (()=> {

})

in home page in the return {
  projects: computed (())
}



wrap the creator profile in a router-link
<router-link :to"{name: 'Profile', params: { id:}}"


in the router add 
path: 'profile/:id'
name: 'profile',
component: loadPage('ProfilePage')


create ProfilePage.vue

export Default ()
setup(){

  const route = useRoute()

  async function getProfile(){
    try {
      await profileService.getProfileById(route.params.id)
    } catch (error) {
      pop.error(error, '[Getting Profile]')
    }
  }

  onMounted(() => {
    getProfile()
  })

  return {}
}

creat a profilservice

class profileService {
  async getProfile(id) {
    const res = await api.get('api/profiles/' + id)
    AppState.activeProfile = new Profile(res.data)
    logger.log('Profile' res.data)
  }
}
export const profileService = new ProfileService()

create Profile Model

export class Profie {
  constructor(data) {

  }
}

on profile page

async function getProjectsByProfile() {
  try {
    await
  } catch (error) {
    Pop.error(error '[Getting Projects]')
  }
}


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


async createAlbum(formData)


instead of putting elvis operators on everything wrap the component or page in a v-if.




back-end side

create Collaborator model

export const Collaborator = new Schema((
  albumId: (type: PbjectId, required: true, ref 'Album'),
  accountId: {type: ObjectId, required: true, ref 'Account'}
  timestamps: true, toJSON { virtuals: true}
))

CollaboratorSchema.virtual('album', {
  localField: 'albumId',
  foreignField: '_id',
  ref: 'Album',
  justOne: true
})

collaboratorSchema.virtual('account', {
    localField: 'albumId',
  foreignField: '_id',
  ref: 'Account',
  justOne: true
})

import model into DbContext

create a controller

collaboratorsController

create a service

class CollaboratorsService{

}

export const collaboratorsService = new CollaboratorsService()






Sockets 
--------------

fresh project

the first thing you want to do/ change useSockets to true
sockets are fancy way to talk to a server 

AuthHandler
SocketService
.emit is how you send messages back and forth

check ws tab in network tab

in the backend
copy and paste the testHandler, paste it into handler folder and rename it to LightHandler

in LightHandler.js

const lightState = {
  on: false
}

.on('GET_LIGHT_STATE', this.getLightState)

async getLightState() {
  this.socket.emit('LIGHT_STATE', lightState)
}

in the frontend in SocketService.js

.on('LIGHT_STATE', this.setLightState)

setLightState(lightState){
  AppState.light = lightState
}

in AppState

light: null

in the homePage

i.mdi.mdi-lightbulb-variant-outline 

Sockets Pt.2
-----------------

in channelsController in server side

add in async create,
 socketProvider.message("s:creating:channel", channel)

 in client side

 in socket service...
 .on("s:creating:channel", this.creatingChannel)


 in onError(e) add...

 creatingChannel(payload) {
  let newChannel = new Channel (payload)
  logger.log("new channel", payload)
  if(!payload) {
    throw new Error("Something went wrong")
  } else {
    if(AppState.account.id != newChannel.creatorId) {
    Pop.toast(`${newChannel.name} has been created`)
    }
    AppState.channels.push(newChannel)
  }
 }


 in server side/MessagesController

 in async create add under let message...
 socketProvider.messageRoom(room, eventName, payload)
  socketProvider.messageRoom(message.roomId.toString(),
"s:creating:message", message
);

back in the SocketService

add another .on("s:creatingmessage", this.creatingMessage)


creatingMessage(payload) {
  logger.log('creating message payload')
  let message = new Message(payload)
  AppState.messages.push(message)
}

in ChannelPage.vue

under onMounted add...

watchEffect(() => {
  route.params.id

})

router.beforeEach((to, from) => {
  logger.log('[TO]', to, "[FROM]", from)
  if(from.name == "Channel") {
    leaveRoom(from.params.id)
  }
})

function leaveRoom(roomId) {
  try {
    let payload = {roomId: roomId}
    socketService.emit("c:leaving:room", payload)
  } catch (error)
  logger.error((error))
  Pop.error(('error')), error.message
}

in RoomHandler.js (it's actually TestHandler) under constructor...

add another .on ("c:leaving:room", this.leavingRoom)


leavingRoom(payload){
  if(!payload.roomId) {
    this.socket.emit("error", {error: "please provide a room Id."})
    return;
  }
  this.socket.leave(payload.roomId);
  this.socket.to(payload.roomId).emit("s:leaving:room", this.user)
} 

back in client side in socketsservice

leavingRoom(payload) {
  if(payload && AppState.account.id != payload.id) {
    pop.toast(`yaddah yaddah`)
  }

}

function joinRoom() {
  try {
    let payload = {roomId : roomId}
    socketService.emit("c:joining:room", payload)
  } catch (error) {

  }
}

in roomHandler

joiningRoom(payload) {
  if(payload.roomId) {
    this.socket.emit("error", {
      error: "wrong"
    })
    return;
  }
  this.socket.join(payload.roomId)
  this.socket.to(payload.roomId).emit("s:joining:room", this.profile)
}


in server/socketService

add .om("s:joiningRoom")

joiningRoom(payload) {
  if(payload && AppState.account.id != payload.id){
    
  }
}


