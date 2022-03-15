<template>
  <main class="main-content">
      <div class="container">
          <h1>Boolflix</h1>
          <div class="search-bar">
              <!-- ogni volta che premo invio o clicco il bottone, verrà invocata la funzione "searchYourMovie"  -->
              <input type="text" id="search-film" placeholder="cerca un film" 
                v-model="movieTitle" @keyup.enter="searchYourMovie()">
              <button @click="searchYourMovie()">Cerca il film!</button>
          </div>
          <div class="films-list">
              <ul>
                  <!-- creo tanti li quanti sono i film dentro l'array moviesList  -->
                  <li v-for="movie in moviesList" :key="movie.id">
                        <span>titolo: {{ movie.title }}</span>
                        <span>titolo originale: {{ movie.original_title }}</span>
                        <span>lingua:
                            <figure>
                                <img :src="movie.original_language" :alt="movie.original_language">
                            </figure> 
                        </span>
                        <span>voto: {{ movie.vote_average }}</span>
                  </li>
              </ul>
          </div>
      </div>
  </main>
</template>

<script>
import axios from 'axios'

export default {

    name: 'myMain',

    data(){
        return{
            moviesList: [],
            movieTitle: '',
        }
    },

    beforeUpdate: function(){
        this.flag();
    },

    methods:{
        searchYourMovie: function(){
            if(this.movieTitle !== ''){
                //chiamata alle API di the movie db che tramite dei query params mi restituisce determinati film
                axios.get(`https://api.themoviedb.org/3/search/movie`,{
                    params:{
                        api_key: 'dbc2947f78dcb3af56135727bc3212eb',
                        query: this.movieTitle,
                        language: 'it-IT',
                    },
                })
                    .then(res => {
                        //metto l'arrey di oggetti(film), dentro il mio array moviesList
                        this.moviesList = res.data.results; 
                        // console.log(this.moviesList);
                        console.log(this.movieTitle)
                    })
            }else{
                this.moviesList = [];
            }
            
        },
        // prova: function(){
        //     console.log(this.movieTitle)
        // }
        flag: function(){
            for(let i = 0; i < this.moviesList.length; i++){
                switch(this.moviesList[i].original_language){
                case 'en':
                    this.moviesList[i].original_language = 'https://media.istockphoto.com/photos/flag-of-england-picture-id854115776?k=6&m=854115776&s=612x612&w=0&h=02VcR134xblIJdequli9a7IpZZX-0qPtGBnTpQZGdFY=';
                    break;
                case 'it':
                    this.moviesList[i].original_language = 'https://th.bing.com/th/id/R.cf7d1bc348e7918da9c165ca33ef7cab?rik=xol8XZyZ7xVmJg&riu=http%3a%2f%2fflags.fmcdn.net%2fdata%2fflags%2fw580%2fit.png&ehk=%2f%2faQEeN1nMh%2fV5xj4%2f%2bS50ZIP3e4Yvlc5fGCNl5I%2fKY%3d&risl=&pid=ImgRaw&r=0&sres=1&sresct=1';
                    break;
                case 'fr':
                    this.moviesList[i].original_language = 'https://th.bing.com/th/id/R.aa26d890249473db99546bcd35839316?rik=ieAZZVEOSMRf%2bw&pid=ImgRaw&r=0';
                    break;
                default:
                    this.moviesList[i].original_language;
                }
            }
            
        }
    },
}
</script>

<style lang="scss" scoped>
    span{
        display: block;
        & figure{
            width: 20px;
            aspect-ratio: 16/9;
            display: inline-block;
        }

        & img {
            max-width: 100%;
        }
    }
</style>