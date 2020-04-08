<template>
  <div class="list"> 
    <section class="item"  v-for="(pokemon, index) in pokemons"
    :key="'poke'+index"
    @click="setPokemonUrl(pokemon.url)"><h1 class="hidden">Pokemon Item</h1>
      <transition name="slide-fade">
    <h3>{{ pokemon.name }}</h3>
      </transition>
    </section> 
  </div>
</template>

<script>
  export default {
    props: [
      'imageUrl',
      'apiUrl'
    ],
    data: () => {
      return {
        pokemons: [],
        nextUrl: '',
        currentUrl: ''
      }
    },
    methods: {
      fetchData() {
        let req = new Request(this.currentUrl);
        fetch(req)
          .then((resp) => {
            if(resp.status === 200)
              return resp.json();
          })
          .then((data) => {
            this.nextUrl = data.next;
            data.results.forEach(pokemon => {
              pokemon.id = pokemon.url.split('/')
                .filter(function(part) { return !!part }).pop();
              this.pokemons.push(pokemon);
            });
          })
          .catch((error) => {
            console.log(error);
          })
      },       
      setPokemonUrl(url) {
        this.$emit('setPokemonUrl', url);
      }
    },
    created() {
      this.currentUrl = this.apiUrl;
      this.fetchData();
    },    
  }
</script>

<style lang="scss" scoped>
  .list {
    display: grid;
    float:left;
    font-size: 25px;
    grid-gap: 5px;
    width: 100%;
    max-width: 500px;
    align-items: center;
    .item {
      height: 50px;
      background-color:rgba(0, 0, 0, 0.673);
      text-align: center;
      text-transform: capitalize;
      transition:all 2s ease;
      cursor: pointer;
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(255, 255, 255, 0.338);

      h3 {
        margin: 0;
      }
      }
    .item:hover
    {
    
    background-color:rgb(26, 26, 26);
      animation: bounce 0.5% linear;
    }
    @keyframes bounce{
      20%{
        transform: translate(-10px);
      }
      40%{
        transform: translate(0px);
      }
      
      
  }
  .slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
    
  }
  
.hidden{
  display:none;
}
  
    
</style>

