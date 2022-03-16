<template>
    <div class="movie-card">
        <figure>
            <img :src="posterMovie()" alt="">
        </figure>
        <span>titolo: {{ currentMovie.title }}</span>
        <span>titolo originale: {{ currentMovie.original_title }}</span>
        <span>lingua: {{ getFlag(currentMovie.original_language) }}</span>
        <span>
            <i class="fa-solid fa-star" v-for="(star, i) in stars" :key="i"></i>
            <i class="fa-regular fa-star" v-for="(notstar, index) in notStars" :key="index"></i>
        </span>
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
    
    data(){
        return{
            numberStars: undefined,
            stars: [],
            notStars: [],
        }
    },

    mounted: function(){
        this.stelle();
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
        },
        stelle: function(){
            console.log(this.currentMovie.vote_average);
            this.numberStar = ((this.currentMovie.vote_average) / 2);
            this.numberStar = Math.ceil(this.numberStar);
            console.log(this.numberStar);
            for(let i = 0; i < this.numberStar; i++){
                this.stars.push(i);
            }
            for(let i = this.numberStar; i < 5; i++){
                this.notStars.push(i);
            }
        },
        
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

    .fa-star{
        color: rgb(255, 208, 0);
    }

</style>