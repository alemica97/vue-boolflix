<template>

    <header>
        <div class="container header 
            d-flex justify-content-center justify-content-md-between 
            align-items-center flex-wrap">

            <figure class="main-logo mb-4 mx-5 mb-md-0 mx-md-0 px-2 flex-shrink-0">
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
        position: fixed;
        z-index: 9999;
        width: 100%;
        background: rgb(0,0,0);
        background: linear-gradient(180deg, rgba(0,0,0,1) 0%, rgba(0,0,0,0.43379901960784315) 65%, rgba(0,0,0,0) 100%);
    }

    .header{
        padding: 30px 15px;
    }

    .main-logo{
        width: 200px;
    }

    .search-bar{
        gap: 15px;

        & input, & button{
            border-radius: 8px;
            border: none;
            font-size: 14px;
            font-weight: 600;
            text-transform: uppercase;
            background-color: rgba(114, 114, 114, 0.253);
            color: #444;
            text-align: center;
        }

        & input{
            padding: 8px 15px;
        }

        & button{
            cursor: pointer;
            padding: 8px 12px;
        }
    }

    @media screen and (max-width: 576px){
        .search-bar{
            gap: 10px;

            & input{
                 padding: 8px 0px;
            }
        }
    }

    @media all and (min-width: 200px){
        *{
            transition: all 300ms;
        }
    }
</style>