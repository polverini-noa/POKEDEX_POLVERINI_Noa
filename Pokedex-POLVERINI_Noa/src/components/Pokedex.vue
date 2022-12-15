<template>
  <!-- div contenant toutes les informations de la pages -->
  <div class="container">
    <!-- logo -->
    <img src="./logo_pokemon.png" alt="" id="logo">

    <!-- appel du composant Pokemon Search -->
    <PokemonSearch @search_Pokemon_Emit="setPokemonSearch"/>

    <!-- Appel du composant Pokemon Detail -->
    <PokemonDetail v-if="visible" v-bind:name="name_pokemon" v-bind:url="detail_url" v-on:close="fermer_Details"/>

    <!-- Appel du composant pokemon list -->
    <PokemonList v-on:pokemon_details_emits="afficher_details" v-bind:search="search" />
  </div>
</template>

<script>

// import 
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {

  // déclaratiion du data
  data: function(){
      return {
        name_pokemon: "",
        detail_url: "",
        visible: false,
        search:'',  // moi
      }
  },

  // déclaration des components
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },

  // déclaration des méthodess
  methods: {
    // méthode pour afficher les détails du pokemon mis en paramètre
    afficher_details(pokemon){
      this.name_pokemon = pokemon.name
      this.detail_url = pokemon.url
      this.visible = true
    },

    // méthode pour fermer les détails du pokemon
    fermer_Details(){
      this.visible = false
    },

    // méthode pour actualiser la recherche de pokemon
    setPokemonSearch(carac){
      this.search = carac
    }
  }
};
</script>

<!-- style de la page -->
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

#logo {
  position: absolute;
  width: 150px;
  left: 10px;
  top: 10px;
}
</style>