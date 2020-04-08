<template>
  <div class="container">
    <section>
      <h4>Pokemon's Fan Guide gives information about the Famous Pokemon's </h4>
    </section>
    <img :src="`../src/assets/pokemon.svg`" alt="logo"><h1>Pokemon's Fan Guide</h1> <img class="poke" :src="`../src/assets/pokemon.svg`" alt="logo">
    
    <PokemonList :imageUrl="imageUrl" :apiUrl="apiUrl" @setPokemonUrl="setPokemonUrl" />
    <PokemonDescription v-if="showDetail" :pokemonUrl="pokemonUrl" :imageUrl="imageUrl" @close="close" />
  </div>
</template>

<script>
  
  import PokemonList from './PokemonList.vue';
  import PokemonDescription from './PokemonDescription.vue';

  export default {
    data: () => {
      return {
        imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
        apiUrl: 'https://pokeapi.co/api/v2/pokemon/?limit=20&offset=20',
        pokemonUrl: '',
        showDetail: false
      }
    },
    components: {
     
      PokemonList,
      PokemonDescription
    },
    methods: {
      setPokemonUrl(url) {
        this.pokemonUrl = url;
        this.showDetail = true;
      },
      close() {
        this.pokemonUrl = '';
        this.showDetail = false;
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css?family=Pangolin&display=swap"');

  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 10px;
    color:rgb(255, 234, 0);
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    background: radial-gradient(rgb(255, 225, 0), rgba(169, 87, 15, 0.749));

    font-family: 'Pangolin', cursive;
    font-size: 1rem;
    font-weight: normal;
  }
  .poke{
    margin-top:-70px;
    margin-left: 800px;
  }
  img{
    margin-top:10px;
    margin-right: 400px;
    height:60px;
    width:70px;
  }
  h1 { 
    margin-top:-36px;
    font-size:40px;
    color: #151514c9;
     }
    h4{
      font-size:30px;
     color: #882d1dc9; 
    }
</style>
