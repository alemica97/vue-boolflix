<template>
    <div class="movie-card">
        <figure>
            <img :src="posterMovie()" alt="">
        </figure>
        <span>titolo: {{ currentMovie.title }}</span>
        <span>titolo originale: {{ currentMovie.original_title }}</span>
        <span>lingua: {{ getFlag(currentMovie.original_language) }}</span>
        <span>voto: {{ currentMovie.vote_average }}</span>
    </div>
</template>

<script>
import getUnicodeFlagIcon from 'country-flag-icons/unicode'

export default {
    name: 'movieCard',

    props:{
        currentMovie:{
            type: Object,
        }
    },
    
    methods:{
        getFlag: function(unicode){

            if(unicode == 'en'){
                unicode = 'gb'
            }
    
            return getUnicodeFlagIcon(unicode.toUpperCase());
        },
        posterMovie: function(){
            return 'http://image.tmdb.org/t/p/w154'+this.currentMovie.poster_path
        }
        
    }
}
</script>

<style lang="scss">
    span{
        display: block;
    }
    .movie-card{
        border: 1px solid black;
        padding: 15px;
    }
</style>