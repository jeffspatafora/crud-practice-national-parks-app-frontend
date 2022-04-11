<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      nationalParks: []
    };
  },
  created: function () {
    this.indexNationalParks();
  },
  methods: {
    indexNationalParks: function () {
      axios.get("/national_parks").then(response => {
        console.log("indexNationalParks", response.data)
        this.nationalParks = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <div v-for="nationalPark in nationalParks" v-bind:key="nationalPark.id">
      <h2>{{ nationalPark.name }}</h2>
      <p>{{ nationalPark.state }}</p>
      <p>{{ nationalPark.size_square_miles }}</p>
      <p>{{ nationalPark.date_founded }}</p>
      <img v-bind:src="nationalPark.map_image" />
    </div>
  </div>
</template>

<style>
img {
  width: 300px;
}
</style>