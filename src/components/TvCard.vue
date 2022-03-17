<template>
    <div class="movie-tv-card">
        <figure>
            <img :src="posterTv" alt="">
        </figure>
        <div class="description-wrapper">
            <div class="card-description">
                <span>titolo: {{ currentTv.name }}</span>
                <span v-if="currentTv.original_name !== currentTv.name">
                    titolo originale: {{ currentTv.original_name }}
                </span>
                <span v-if="trueFlag(currentTv.original_language)">
                    lingua: {{ getFlag(currentTv.original_language) }}
                </span>
                <span v-else>lingua: {{currentTv.original_language}}</span>
                <span>
                    <i :class=" roundVote > i ? 'fa-solid fa-star' : 'fa-regular fa-star'"  
                        v-for="(star, i) in 5" :key="i"></i>
                </span>
                <p v-if="currentTv.overview" class="overview">
                    overview: {{ currentTv.overview }}
                </p>
                <p v-else class="overview">
                    overview: Questo contenuto non ha una descrizione. 
                </p>
            </div>
        </div>
    </div>
</template>

<script>
import getUnicodeFlagIcon from 'country-flag-icons/unicode'
import { hasFlag } from 'country-flag-icons'

export default {
    name: 'tvCard',

    props:{
        currentTv:{
            type: Object,
        }
    },

    computed: {
        roundVote: function(){
            return Math.ceil((this.currentTv.vote_average) * 0.5)
        },

        posterTv: function(){
            if(this.currentTv.poster_path !== null){
                return 'http://image.tmdb.org/t/p/w342'+this.currentTv.poster_path
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