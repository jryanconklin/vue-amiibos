<template>
  <div class="col-lg-4 col-md-6 py-2">
    <div class="card h-100 bg-shiny">
      <div class="card-header text-light">
        <h4 class="text-truncate">{{ amiibo.name }}</h4>
        <h5>Series: {{ amiibo.amiiboSeries }}</h5>
      </div>
      <!--<h6 class="card-header py-3">{{ amiibo.amiiboSeries }} | {{ amiibo.name}}</h6>-->
      <div class="card-img-top m-1">
        <img class="img-fluid" :src="amiibo.image" :alt="amiibo.name">
      </div>
      <div class="card-body d-flex flex-column mb-auto">
        <div class="card-title rounded mb-1 p-1 text-center"><span class="text-light">Release Dates</span></div>
        <div class="mb-2">
          <ul class="list-group list-group-flush" v-for="(date, index) in amiibo.release" :key="index">
            <li class="list-group-item"><span class="text-uppercase font-weight-bold">{{ index }}:</span> {{ date ? date : 'No Release Date Available' }}</li>
          </ul>
        </div>
        <!-- @TODO Include Affiliate ID for Amazon in Link-->
        <a :href="'https://www.amazon.com/s?k=' + amiibo.name + '+amiibo'" class="btn btn-success mt-auto">Buy on Amazon</a>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'AmiiboCard',
  props: {
    amiibo: {
      type: Object,
      required: true,
    }
  },
}
</script>

<style scoped>

.card-title {
  background-color: #d16ba5;
}

.card-img-top {
  width: 100%;
  height: 20vh;
  object-fit: cover;
}
</style>
