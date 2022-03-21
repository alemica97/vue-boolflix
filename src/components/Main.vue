<template>
    <main>  
        <div class="container-lg px-3 d-flex flex-column">                           
            <div class="list-wrapper">
                <h1 v-if="movieList.length != 0" class="mt-4">film</h1>
                <div class="films-list d-flex flex-wrap justify-content-center justify-content-md-start">
                    <movieCard 
                    class="movie-card"
                    v-for="(movie, index) in movieList" 
                    :key="index" :currentMovie="movie"/>
                </div>
            </div>
            <div class="list-wrapper">
                <h1 v-if="propsTvList.length != 0" class="mt-4">serie</h1>
                <div class="tv-list d-flex flex-wrap justify-content-start"> 
                    <tvCard 
                    class="tv-card"
                    v-for="(tv, i) in propsTvList" 
                    :key="i" :currentTv="tv"/>
                </div>
            </div>            
        </div>
    </main>
</template>

<script>
import movieCard from './MovieCard.vue'
import tvCard from './TvCard.vue'

export default {

    name: 'myMain',

    components:{
        movieCard,
        tvCard,
    },

    props: {
        movieList: {
            type: Array,
        },
        propsTvList: {
            type: Array,
        }
    },


}
</script>

<style lang="scss" scoped>

    .container-lg{
        padding: 150px 0;
    }

    .films-list, .tv-list{
        padding: 30px;
        gap: 15px;
    }

    h1{
        color: #DC1A28;
        text-align: center;
        text-transform: uppercase;
        font-weight: 700;
        color: rgb(95, 95, 95);
    }

    .movie-card, .tv-card{
        width: calc((100% - 60px) / 5);
        min-width: 200px;
    }

    //media query
    @import '../assets/scss/mediaQuery.scss';
</style>