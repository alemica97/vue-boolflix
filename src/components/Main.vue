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
                      <span>lingua: {{ movie.original_language }}</span>
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
    methods:{
        searchYourMovie: function(){
            //chiamata alle API di the movie db che tramite dei query params mi restituisce determinati film
            axios.get(`https://api.themoviedb.org/3/search/movie/?api_key=dbc2947f78dcb3af56135727bc3212eb&language=it-IT&query=${this.movieTitle}`)
                .then(res => {
                    // console.log(res.data.results);
                    //metto l'arrey di oggetti(film), dentro il mio array moviesList
                    this.moviesList = res.data.results; 
                    // console.log(this.moviesList);
                    console.log(this.movieTitle)
                })
        },
        // prova: function(){
        //     console.log(this.movieTitle)
        // }
    },
}
</script>

<style lang="scss" scoped>
    span{
        display: block;
    }
</style>