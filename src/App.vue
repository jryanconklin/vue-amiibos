<template>
  <div class="page">

    <!-- Jumbotron as Own Component -->
    <div class="jumbotron jumbotron-fluid bg-shiny">
      <div class="container text-light">
        <h1 class="display-4">AmiiboSource</h1>
        <p class="lead">Your source for searchable amiibos.</p>
      </div>
    </div>

    <div id="app" class="container">
      <form>
        <div class="form-group">
          <label for="amiibo-search" class="h2">Amiibo Filter</label>
          <input v-model="amiiboSearch" v-on:input="updateAmiibos(amiiboSearch)" type="text" class="form-control" id="amiibo-search" placeholder="Character Name">
        </div>
      </form>

      <h2>Search Results</h2>
      <div class="row">
        <AmiiboCard v-for="(amiibo, index) in amiibos" :amiibo="amiibo" :key="index"></AmiiboCard>
      </div>

    </div>
  </div>
</template>

<script>

const API_URL = 'http://www.amiiboapi.com/api/amiibo/';

import AmiiboCard from './components/AmiiboCard.vue';

export default {
  name: 'app',
  components: {
    AmiiboCard,
  },


  data() {
    return {
      amiibos: [],
      amiibosOriginal: [],
      amiiboSearch: '',
    }
  },

  created() {
    this.initAmiibos();
  },

  methods: {
    async initAmiibos() {
      let data = await (await fetch(API_URL)).json();
      this.amiibos = await (data.amiibo);
      this.amiibosOriginal = await (data.amiibo);
    },

    getAllAmiibos() {
      return this.amiibos = this.amiibosOriginal;
    },

    updateAmiibos(input) {
      if (!input.length) {
        this.getAllAmiibos();
      } else {
        this.amiibos = this.amiibos.filter(function(item) {
          return item.name.toLowerCase().match(input.toLowerCase())
        })
      }
    },

  }, // End Methods

} // End Export

</script>

<style>
@import url("https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css");

.bg-shiny {
  background-image: linear-gradient(to right top, #d16ba5, #c777b9, #ba83ca, #aa8fd8, #9a9ae1, #8aa7ec, #79b3f4, #69bff8, #52cffe, #41dfff, #46eefa, #5ffbf1);
}

</style>
