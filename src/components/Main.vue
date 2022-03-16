<template>
    <main class="container">
        <div class="lists-wrapper">
            <h1>Film</h1>
            <div class="films-list">
                <movieCard v-for="(movie, index) in movieList" :key="index" :currentMovie="movie"/>
            </div>
            <h1>Serie</h1>
            <div class="tv-list">
                <tvCard v-for="(tv, i) in propsTvList" :key="i" :currentTv="tv"/>
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
    span{
        display: block;
    }

    ul,li{
        list-style-type: none;
    }

    li{
        border: 1px solid black;
        padding: 10px;
    }

    .container{
        margin: 0 auto;
        width: 1400px;
    }

    .films-list h1, .tv-list h1{
        text-align: left;
    }

    .films-list, .tv-list{
            display: flex;
            justify-content: flex-start;
            flex-wrap: wrap;
            gap: 20px;
        }


    .lists-wrapper{
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: flex-start;
        flex-wrap: wrap;
        text-align: left;
        margin-top: 30px;
        gap: 50px;
    }
</style>