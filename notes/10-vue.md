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
