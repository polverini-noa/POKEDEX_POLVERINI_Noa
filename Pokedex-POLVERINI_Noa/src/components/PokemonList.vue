<template>
  <!-- div qui va contenir tous les pokémons -->
  <div class="list">
    <!-- déclaration d'un article auquel on va associer une boucle for qui va boucler sur les pokemons -->
    <article v-for="pokemon in pokemonsFiltered" v-bind:key="pokemon.name" v-on:click="showPokemonDetail(pokemon)">
      <!-- Nom du pokemon -->
      <h3>{{pokemon.name}}</h3>
      <!-- image du pokemon -->
      <img v-bind:src="pokemon_img_url+pokemon.name+'.png'" alt="">
    </article>
  </div>
</template>

<script>
// import
import axios from 'axios';
// déclaration de la constante pour utiliser la fonction .filter de lodash
const _ = require("lodash"); 

export default {
  // déclaration d'un beforeMount qui va renvoyer la liste des pokemons
  mounted() {
    axios
      .get('https://pokeapi.co/api/v2/pokemon')
      .then((response) => {
        this.liste_pokemon = response.data.results
      })
  },

  // création du data
  data: function(){
      return {
        liste_pokemon: null,
        pokemon_img_url: "https://img.pokemondb.net/sprites/bank/normal/",
      }
  },

  // déclaration des props
  props : ["search"],
  
  // déclaration des méthodes 
  methods: {
    // méthodes pour afficher les détails du pokemon (va envoyer le signal au fichier principal Pokedex.vue)
    showPokemonDetail (pokemon) { 
      this.$emit("pokemon_details_emits", pokemon)
    },
  },

  // déclaration du computed pour pouvoir réaliser la recherche.
  computed: {
    // fonction qui va sois afficher tous les pokemon si la barre de recherche est vide, sinon il va renvoyer une liste de pokemon dont le nom comporte les lettres entrés dans la zone de recherche.
    pokemonsFiltered: function(){ 
      if (this.search == undefined){
        return this.liste_pokemon
      }
  
      else{
        return _.filter(this.liste_pokemon, pokemon => pokemon.name.includes(this.search.toLowerCase()))
       }
    }
  },
};
</script>

<!-- style de la page -->
<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 900px;
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

