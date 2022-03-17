<template>

    <header>
        <div class="container header 
            d-flex justify-content-center justify-content-md-between 
            align-items-center flex-wrap">

            <figure class="main-logo mb-3 mx-5 mb-md-0 px-2">
                <img :src="netflixLogo" alt="">
            </figure>

            <div class="search-bar
                d-flex flex-grow-1 justify-content-center justify-content-md-end">
                <!-- ogni volta che premo invio o clicco il bottone, verrà invocata la funzione "searchYourMovie"  -->
                <input type="text" id="search-film" placeholder="cerca un film" 
                    v-model="movieTitle" @keyup.enter="$emit('fetchTitle', movieTitle)">
                <button @click="$emit('fetchTitle', movieTitle)"><i class="fa-solid fa-magnifying-glass"></i></button>
            </div>

        </div>
    </header>
    
</template>

<script>

export default {
  name: 'myHeader',

  data(){
      return{
        movieTitle: '',
        netflixLogo: 'https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png',
      }
  },
}
</script>

<style lang="scss" scoped>

    header{
        background-color: black;
    }
    .header{
        padding: 20px 15px;
    }

    .main-logo{
        width: 200px;
    }

    .search-bar{
        gap: 15px;

        & input, & button{
            border-radius: 8px;
            border: none;
            font-size: 15px;
        }

        & input{
            padding: 8px 15px;
        }

        & button{
            cursor: pointer;
            padding: 8px 12px;
        }
    }
</style>