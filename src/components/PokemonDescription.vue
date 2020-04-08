<template>
  <div class="container">
      <h4 class="hidden">Container</h4>
    <transition name="bounce" >
    <div class="detail" v-if="show">
      <button class="close" @click="close">X</button>
      <section v-if="pokemon" class="image">
       <h2> <img :src="imageUrl + pokemon.id + '.png'" alt="Pokemon Image" ></h2>
      </section>
      <section v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <section class="item">
          <h2><b>Height:</b> {{ pokemon.height }}</h2>
        </section>
        <section class="item">
          <h2><b>Weight:</b> {{ pokemon.weight }}</h2>
        </section>
        <section class="item">
          <h2>Base Experience: {{ pokemon.base_experience }} XP </h2>
        </section>
               
        <h3><b>Pokemon Abilities:</b></h3>
        <div class="abilities">
          <section class="ability" v-for="(value, index) in pokemon.abilities" :key="'value'+index">
           <h4 class="hidden">Pokemon Abilities List</h4> {{ value.ability.name }}
          </section>
        </div>
       <h3><b>Pokemon Types:</b></h3>
        <div class="types">
          <section class="type" v-for="(value, index) in pokemon.types" :key="'value'+index">
             <h4 class="hidden">Pokemon Types List</h4>{{ value.type.name }}
          </section>
        </div>
      </section>
    </div>
  </transition>   
  </div>
 
</template>

<script>
  export default {
    props: [
      'pokemonUrl',
      'imageUrl'
    ],
    
    data: () => {
      return {
          
        show: false,
        pokemon: {}
      }      
    },
    methods: {
      fetchData() {
        let req = new Request(this.pokemonUrl);
        fetch(req)
          .then((res) => {
            if(res.status === 200)
              return res.json();
          })
          .then((data) => {
            this.pokemon = data;
            this.show = true;
          })
          .catch((error) => {
            console.log(error);
          })
      },
      close() {
        this.$emit('close');
      }
    },
    created() {
      this.fetchData();
    }
  }
</script>

<style lang="scss" scoped>
  .container {
    //transition:all 2s ease;
    padding: 100px 5px 5px;
    width: calc(100% - 10px);
    height: calc(100vh - 10px);
    display: flex;
    justify-content: center;
    //align-items: flex-start;
    position: fixed;
    background-color: rgba(36, 33, 33, 0.851);
    top: 0;
    left: 0;
    background: rgba($color: #000000, $alpha: .7);

    .detail {
      background-color: #000000;
      width: 100%;
      margin-bottom:130px;
      max-width: 510px;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      position: relative;
      padding: 50px 0 0;
      background-color: rgba(187, 172, 104, 0.851);
     
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(215, 210, 210, 0.2);
    
      .image {
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        top: 0px;
        width: 130px;
        height: 130px;
        background-color:rgba(199, 166, 109, 0.927);
       
        overflow: hidden;
        box-shadow: 0 15px 30px rgba(52, 51, 51, 0.2),
                    0 10px 10px rgba(131, 128, 128, 0.2);
      }

      h2 {
        text-transform: capitalize;
      }

      .data {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        flex-direction: column;
        width: 100%;
        margin-bottom: 40px;
        color:rgb(255, 234, 0);
        .item {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px;
          //margin-bottom: 20px;
          float: left;
          
          
        }

        h3 {
          width: 80%;
          max-width: 400px;
        
          
        }
        b{
          font-size:20px;
        }
        .types, .abilities {
          display: flex;
          justify-content: flex-start;
          flex-wrap: wrap;
          width: 90%;
          max-width: 400px;
          
          .type, .ability {
            margin: 0 10px 10px 0;
            padding: 5px 10px; 
            color: #fff;
            font-size: 1rem;
            letter-spacing: 2px;
            text-transform: capitalize;  
          }

          .type { background-color: rgb(80, 15, 10); }
          .ability { background-color: rgb(60, 199, 21); }
        }
      }

      .close {
        outline: 1px;
        border: 2px;
        border-color: white;
        box-shadow: 0 15px 30px rgba(52, 51, 51, 0.2),
                    0 10px 10px rgba(129, 59, 59, 0.2);
        background-color: rgb(55, 53, 53);
        color: #efefef;
        padding: 10px 20px;
        margin-bottom: 20px;
        margin-right:302px;
        font-size: 1.2rem;
        cursor: pointer;
      }
    }

   
  }
  .bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-in .5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
.hidden{
    display: none;
}

</style>
