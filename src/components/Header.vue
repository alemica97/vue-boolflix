<template>

    <header>
        <div class="main-logo">
            <h1>Boolflix</h1>
        </div>
        <div class="search-bar">
            <!-- ogni volta che premo invio o clicco il bottone, verrà invocata la funzione "searchYourMovie"  -->
            <input type="text" id="search-film" placeholder="cerca un film" 
                v-model="movieTitle" @keyup.enter="$emit('fetchTitle', movieTitle)">
            <button @click="$emit('fetchTitle', movieTitle)">Cerca il film!</button>
        </div>
    </header>
    
</template>

<script>

export default {
  name: 'myHeader',

  data(){
      return{
        movieTitle: '',
      }
  },
}
</script>

<style lang="scss">

</style>