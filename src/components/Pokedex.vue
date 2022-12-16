<!--
CARON Samuel 2019-10-29 15:49:52
Pokedex.vue
-->

<template>
  <div class="container">
    <PokemonSearch v-on:searchPokemonEmit="helpSearch"/>
    <PokemonDetail v-if="this.display==true" :pokemonUrl="this.pokemon.url" :imageUrl="this.pokemon.image" v-on:CloseDetail="close"/>
    <PokemonList v-on:showPokemonDetailEmit="show" :pokemonSearch="this.search"/>
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {
  // Components
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },

  // Methods
  methods: {
    // Close pokemon detail
    close: function() {
      console.log('fermer');
      this.display = false;
    },
    // Show pokemon detail
    show: function(pokemon){
      console.log(pokemon)
      this.pokemon = pokemon;
      this.display = true;
    },
    // Help search pokemon
    helpSearch: function (search) {
      this.search = search
      console.log(this.search)
    },
  },

  // Data
  data: function () {
    return {
      pokemon : [],
      display: false,
      search: "",
    };
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>