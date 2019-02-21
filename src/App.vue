<template>
  <div class="page">

    <!-- Jumbotron: Simple Site Header -->
    <div class="jumbotron jumbotron-fluid bg-shiny">
      <div class="container text-light">
        <h1 class="display-4">AmiiboSource</h1>
        <p class="lead">Your source for searchable amiibos.</p>
      </div>
    </div>

    <!-- Search Filters: Provide Searchable Fields for Amiibos -->
    <div id="app" class="container">
      <h2>Search Filters</h2>
      <form id="amiibo-search-form" v-on:submit.prevent>
        <div class="row">
          <!-- Character Search: Input String Search for Amiibo Characters -->
          <div class="col">
            <input v-model="characterSearch"
              v-on:input="
              updateAmiibos(characterSearch, searchType = 'name')"
              type="text" class="form-control"
              id="amiibo-character-search"
              placeholder="Character Name"
            >
          </div>

          <!-- Series Filter: Dropdown List of Amiibo Series -->
          <div class="col">
            <select v-model="seriesSelect"
              id="amiibo-series-select"
              class="custom-select"
              v-on:change=
              "updateAmiibos(seriesSelect, searchType = 'amiiboSeries')"
            >
              <option value="">Select an Amiibo Series</option>
              <option v-for="(amiiboSeries, index) in amiiboSeriesUnique"
                :key="index"
                v-bind:value="amiiboSeries"
              >{{ amiiboSeries }}</option>
            </select>
          </div>

        </div> <!-- End Row -->

        <!-- Search Field Reset Button: Resets Amiibo Array to OG State -->
        <!-- @TODO Combine Clear Button Functions -->
        <button
          v-on:click="resetForm"
          class="btn btn-success m-1"
        >
          Clear Filters
        </button>
        <button
          v-on:click="resetAmiibos"
          class="btn btn-success m-1"
        >
          Reset Amiibos
        </button>
      </form>

      <!-- Amiibo Card Results: See ./components/AmiiboCard.vue -->
      <h2>Search Results</h2>
      <div class="row">
        <AmiiboCard
          v-for="(amiibo, index) in amiibos" :amiibo="amiibo"
          :key="index"
        ></AmiiboCard>
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
      characterSearch: '',
      seriesSelect: '',
      searchType: '',
    }
  },

  computed: {
    amiiboSeriesUnique () {
      return [...new Set(this.amiibos.map(a => a.amiiboSeries))]
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
      return this.amiibosOriginal;
    },

    updateAmiibos(input, searchType) {
      if (!input.length) {
        this.amiibos = this.getAllAmiibos();
      } else {
        this.amiibos = this.amiibosOriginal.filter(function(item) {
          return item[searchType].toLowerCase().match(input.toLowerCase())
        })
      }
    },

    resetForm() {
      let form = document.getElementById('amiibo-search-form');
      form.reset();
    },

    resetAmiibos() {
      this.amiibos = this.getAllAmiibos();
    },

  }, // End Methods

} // End Export

</script>

<style>
@import url("https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css");

.bg-shiny {
  background-image:
    linear-gradient(
    to right top,
    #d16ba5,
    #c777b9,
    #ba83ca,
    #aa8fd8,
    #9a9ae1,
    #8aa7ec,
    #79b3f4,
    #69bff8,
    #52cffe,
    #41dfff,
    #46eefa,
    #5ffbf1
  );
}

</style>
