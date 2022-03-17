<template>
    <main class="container-fluid px-3">
        <div class="lists-wrapper">
            <h1>Film</h1>
            <div class="films-list row d-flex justify-content-center g-4">
                <movieCard 
                class="movie-card p-0"
                v-for="(movie, index) in movieList" 
                :key="index" :currentMovie="movie"/>
            </div>
            <h1>Serie</h1>
            <div class="tv-list row d-flex g-4">
                <tvCard 
                class="tv-card p-0"
                v-for="(tv, i) in propsTvList" 
                :key="i" :currentTv="tv"/>
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
    main{
        background-color: #333;
    }

    span{
        display: block;
    }
    // .films-list, .tv-list{
    //         display: flex;
    //         justify-content: flex-start;
    //         flex-wrap: wrap;
    //         gap: 20px;
    //     }


    // .lists-wrapper{
    //     display: flex;
    //     flex-direction: column;
    //     justify-content: space-around;
    //     align-items: flex-start;
    //     flex-wrap: wrap;
    //     text-align: left;
    //     margin-top: 30px;
    //     gap: 50px;
    // }

    .movie-card, .tv-card{
        width: calc((100% - 80px) / 5);
        min-width: 200px;
    }
</style>