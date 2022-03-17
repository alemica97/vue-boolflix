<template>
    <div class="tv-card">
        <figure>
            <img :src="posterTv" alt="">
        </figure>
        <span>titolo: {{ currentTv.name }}</span>
        <span>titolo originale: {{ currentTv.original_name }}</span>
        <span v-if="trueFlag(currentTv.original_language)">
            lingua: {{ getFlag(currentTv.original_language) }}
        </span>
        <span v-else>lingua: {{currentTv.original_language}}</span>
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
                return 'http://image.tmdb.org/t/p/w185'+this.currentTv.poster_path
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

    .tv-card{
        border: 1px solid black;
        padding: 15px;
    }

    figure{
        aspect-ratio: 9/16;
    }
</style>