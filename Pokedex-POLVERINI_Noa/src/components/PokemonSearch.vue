<template>
  <!-- div contenant la barre de recherche -->
  <div class="searchbar">
    <!-- input pour rentrer le nom du pokemon -->
    <input type="text" v-model="event_search_bar" placeholder="Rechercher un pokémon">   
  </div>
</template>

<script>
export default {
  // création du data
  data() {
    return {
      event_search_bar : "",
    }
  },

  // création du watch qui va envoyer un signal au fichier principal Pokedex.vue à chaque fois que le contenu de la barre de recherche va changé.
  watch: {
    event_search_bar : function() {
      this.$emit("search_Pokemon_Emit", this.event_search_bar)
    }
  },
};
</script>

<!-- style de la page -->
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
