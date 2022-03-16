<template>
    <div class="tv-card">
        <figure>
            <img :src="posterTv()" alt="">
        </figure>
        <span>titolo: {{ currentTv.name }}</span>
        <span>titolo originale: {{ currentTv.original_name }}</span>
        <span>lingua: {{ getFlag(currentTv.original_language) }}</span>
        <span>voto: {{ currentTv.vote_average }}</span>
    </div>
</template>

<script>
import getUnicodeFlagIcon from 'country-flag-icons/unicode'

export default {
    name: 'tvCard',

    props:{
        currentTv:{
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
        posterTv: function(){
            return 'http://image.tmdb.org/t/p/w154'+this.currentTv.poster_path
        }
    }
}
</script>

<style lang="scss">
    span{
        display: block;
    }

    .tv-card{
        border: 1px solid black;
        padding: 15px;
    }
</style>