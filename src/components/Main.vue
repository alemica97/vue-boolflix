<template>
  <main class="main-content">
      <div class="container">
          <h1>Boolflix</h1>
          <div class="search-bar">
              <input type="text" id="search-film" placeholder="cerca un film">
              <button>VAI!</button>
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
        }
    },
    created(){
        //chiamata alle API di the movie db che tramite dei query params mi restituisce determinati film
        axios.get('https://api.themoviedb.org/3/search/movie/?api_key=dbc2947f78dcb3af56135727bc3212eb&language=it-IT&query=spiderman')
            .then(res => {
                // console.log(res.data.results);
                //metto l'arrey di oggetti(film), dentro il mio array moviesList
                this.moviesList = res.data.results; 
                // console.log(this.moviesList);
            })
    }
}
</script>

<style lang="scss" scoped>
    span{
        display: block;
    }
</style>