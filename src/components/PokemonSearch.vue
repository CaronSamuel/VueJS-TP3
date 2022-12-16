<!--
CARON Samuel 2019-10-29 15:49:52
PokemonSearch.vue
-->
<template>
  <div class="searchbar">
    <input type="text" placeholder="Search..." v-model="search">
  </div>
</template>

<script>
export default {
  // Name
  name: "PokemonSearch",

  // Data
  data: function () {
    return {
      search : "",
    }
  },

  watch: {
    // Watch search
    search: function () {
      this.$emit('searchPokemonEmit', this.search);
    }
  }
};
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 510px;
  padding-bottom: 20px;
}
input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
</style>
