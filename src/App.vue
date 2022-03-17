<template>
  <div id="app">
    <myHeader @fetchTitle="saveTitleFromHeader"/>
    <myMain :movieList="moviesList" :propsTvList='tvList' />
  </div>
</template>

<script>
import axios from 'axios'
import myHeader from './components/Header.vue'
import myMain from './components/Main.vue'

export default {
  name: 'App',

  components: {
    myMain,
    myHeader,
  },
  
  data() {
    return{
      savedTitle: "",
      moviesList: [],
      tvList: [],
    }
  },
  methods: {
    saveTitleFromHeader: function(movieTitle){
        this.savedTitle = movieTitle;

        this.searchYourMovie();
        this.searchTv();
    },
    //FILM
    searchYourMovie: function(){
            if(this.savedTitle !== ''){
                //chiamata alle API di the movie db che tramite dei query params mi restituisce determinati film
                axios.get(`https://api.themoviedb.org/3/search/movie`,{
                    params:{
                        api_key: 'dbc2947f78dcb3af56135727bc3212eb',
                        query: this.savedTitle,
                        language: 'it-IT',
                    },
                })
                    .then(res => {
                        //metto l'arrey di oggetti(film), dentro il mio array moviesList
                        this.moviesList = res.data.results; 
                        console.log('Hai cercato: ',this.savedTitle);
                        console.log('Lista dei film: ',this.moviesList)
                    })
            }else{
                this.moviesList = [];
            }
            
        },
        //SERIE TV
        searchTv: function(){
            if(this.savedTitle !== ''){
                axios.get(`https://api.themoviedb.org/3/search/tv`,{
                    params:{
                        api_key: 'dbc2947f78dcb3af56135727bc3212eb',
                        query: this.savedTitle,
                        language: 'it-IT',
                    },
                })
                    .then(res => {
                        //metto l'arrey di oggetti(film), dentro il mio array moviesList
                        this.tvList = res.data.results; 
                        console.log('Lista delle serie tv: ',this.tvList);
                    })
            }else{
                this.tvList = [];
            }
            
        },
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.css';
@import './assets/scss/common.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

</style>
