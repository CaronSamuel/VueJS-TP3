<!--
CARON Samuel 2019-10-29 15:49:52
PokemonList.vue
-->
<template>
  <div class="list">
    <article v-for="pokemon in filteredPokemons" v-bind:key="pokemon.name" v-on:click="showPokemonDetail(pokemon)">
      <img :src="pokemon.image" alt="">
      <h3>{{ pokemon.name }}</h3>
    </article>
  </div>
</template>

<script>
import axios from '../../node_modules/axios'
import API from '../config/config.json'

export default {
  // Name
  name : 'PokemonList',

  // Props
  props: ['pokemonSearch'],

  beforeMount(){
    // appel de l'api pour récuperer la liste des characters
    axios.get(API["API_URL"] + "/pokemon")
      .then((e)=>{
        // sur le retour on stock la data dans caracters
        this.pokemons = e.data.results;
        
        // Permet de récupérer les images des pokemons selon leur nom
        for (let i = 0; i < this.pokemons.length; i++) {
          const elt = this.pokemons[i];
          elt.image = API["IMG_URL"] + elt.name + ".png"
        }
      })
  },

  // Data
  data: function () {
    return {
      // datastore
      pokemons: [],
    };
  },

  // Method
  methods: {
    // Show pokemon detail
    showPokemonDetail : function(pokemon){
      this.$emit('showPokemonDetailEmit', pokemon);
    }
  },

  // Computed
  computed: {
    // Filter pokemons
    filteredPokemons: function () {
      return this.pokemons.filter((pokemon) => {
        return pokemon.name.match(this.pokemonSearch)
      })
    }
  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

