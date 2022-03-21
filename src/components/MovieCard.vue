<template>
    <div class="movie-tv-card">
        <figure>
            <img :src="posterMovie" alt="">
        </figure>
        <div class="description-wrapper">
            <div class="card-description">
                <span>titolo: {{ currentMovie.title }}</span>
                <!-- faccio un controllo, faccio vedere il titolo originale solo se è diverso dal titolo -->
                <span v-if="currentMovie.original_title !== currentMovie.title">
                    titolo originale: {{ currentMovie.original_title }}
                </span>
                <!-- faccio un controllo, se la bandiera è presente la mostro, altrimenti faccio vedere solo la sigla -->
                <span v-if="trueFlag(currentMovie.original_language)">
                    lingua: {{ getFlag(currentMovie.original_language) }}
                </span>
                <span v-else>lingua: {{currentMovie.original_language}}</span>
                <span>
                    <i :class=" roundVote > i ? 'fa-solid fa-star' : 'fa-regular fa-star'"  
                        v-for="(star, i) in 5" :key="i"></i>
                </span>
                <div class="overview-wrapper">
                    <p v-if="currentMovie.overview" class="overview">
                    overview: {{ currentMovie.overview }}
                    </p>
                    <p v-else class="overview">
                        overview: Questo contenuto non ha una descrizione.
                    </p>
                </div>
            </div>
        </div>
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
                return 'http://image.tmdb.org/t/p/w342'+this.currentMovie.poster_path
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
    //tutto dentro card.scss
    @import '../assets/scss/cards.scss';
</style>