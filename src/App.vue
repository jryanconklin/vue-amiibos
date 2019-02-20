<template>
  <div class="page">
    <div id="app" class="container">
      <h1>Amiibo Search</h1>

      <!-- Amiibo Search Filter: Set as Separate Component Eventually -->
      <!-- Capture User Input and Filter by amiibo array by amiibo.name in results -->
      <form>
        <div class="form-group">
          <label for="amiibo-search" class="h2">Amiibo Filter</label>
          <!-- @TODO Update Placeholder Text as Autocomplete from ammiibo array -->
          <input v-model="amiiboSearch" v-on:input="updateAmiibos(amiiboSearch)" type="text" class="form-control" id="amiibo-search" placeholder="Amiibo Name">
        </div>
      </form>
      <!-- Amiibo Search Filter: Set as Separate Component Eventually -->

      <h2>Search Results</h2>
      <!-- Amiibo Search Results: Set as Separate Component Eventually -->
      <div class="row">
        <div class="col-lg-4 col-md-6 py-2" v-for="(amiibo, index) in amiibos" :key="index">
          <div class="card h-100">
            <h6 class="card-header">{{ amiibo.amiiboSeries }} | {{ amiibo.name }}</h6>
            <div class="card-img-top m-1">
              <img class="img-fluid" :src="amiibo.image" :alt="amiibo.name">
            </div>
            <div class="card-body d-flex flex-column mb-auto">
              <div class="card-title rounded mb-1 p-1 text-center"><span class="text-light">Release Dates</span></div>
              <div class="mb-2">
                <ul class="list-group list-group-flush" v-for="(date, index) in amiibo.release" :key="index">
                  <li class="list-group-item"><span class="text-uppercase font-weight-bold">{{ index }}:</span> {{ date }}</li>
                </ul>
              </div>
              <!-- @TODO Include Affiliate ID for Amazon in Link-->
              <a :href="'https://www.amazon.com/s?k=' + amiibo.name + '+amiibo'" class="btn btn-success mt-auto">Buy on Amazon</a>
            </div>
          </div>
        </div>
      </div>
      <!-- End Amiibo Search Results: Set as Separate Component Eventually @see AmiiboCards.vue -->

    </div>
  </div>
</template>

<script>

const API_URL = 'http://www.amiiboapi.com/api/amiibo/';

export default {
  name: 'app',

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

  },

}
</script>

<style>
@import url("https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css");
.card {
  background-image: linear-gradient(to right top, #d16ba5, #c777b9, #ba83ca, #aa8fd8, #9a9ae1, #8aa7ec, #79b3f4, #69bff8, #52cffe, #41dfff, #46eefa, #5ffbf1);
}

.card-title {
  background-color: #d16ba5;
}

.card-img-top {
  width: 100%;
  height: 20vh;
  object-fit: cover;
}
</style>
