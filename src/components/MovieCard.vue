<template>
    <div class="movie-card">
        <figure>
            <img :src="posterMovie" alt="">
        </figure>
        <span>titolo: {{ currentMovie.title }}</span>
        <span>titolo originale: {{ currentMovie.original_title }}</span>
        <span v-if="trueFlag(currentMovie.original_language)">
            lingua: {{ getFlag(currentMovie.original_language) }}
        </span>
        <span v-else>lingua: {{currentMovie.original_language}}</span>
        <span>
            <i :class=" roundVote > i ? 'fa-solid fa-star' : 'fa-regular fa-star'"  
                v-for="(star, i) in 5" :key="i"></i>
        </span>
    </div>
</template>

<script>
import getUnicodeFlagIcon from 'country-flag-icons/unicode'
import { hasFlag } from 'country-flag-icons'

export default {
    name: 'movieCard',

    props:{
        currentMovie:{
            type: Object,
        },
    },

    computed: {
        roundVote: function(){
            return Math.ceil((this.currentMovie.vote_average) * 0.5)
        },
        
        posterMovie: function(){
            if(this.currentMovie.poster_path !== null){
                return 'http://image.tmdb.org/t/p/w185'+this.currentMovie.poster_path
            }else{
                return 'https://th.bing.com/th/id/OIP.G4dvQDdiYY8L202JaqMbHgHaHa?pid=ImgDet&rs=1'
            }  
        }, 
    },

    methods:{
        getFlag: function(unicode){

            if(unicode == 'en'){
                unicode = 'gb'
            }
            return getUnicodeFlagIcon(unicode.toUpperCase());
        },

        trueFlag: function(unicode){

            if(unicode == 'en'){
                unicode = 'gb'
            }

            if(hasFlag(unicode.toUpperCase())){
                return true
            }else{
                return false
            }
        },
    
    }
}
</script>

<style lang="scss" scoped>
    span{
        display: block;
    }
    .movie-card{
        border: 1px solid black;
        padding: 15px;
    }

    figure{
        aspect-ratio: 9/16;
    }
</style>