<template>
  <div class="col-lg-3 col-md-4 col-sm-6 py-2">
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
