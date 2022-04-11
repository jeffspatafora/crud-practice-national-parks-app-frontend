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
      })
    },
    createNationalPark: function () {
      console.log("in create");
      let newNationalParkParams = {
        name: "Grand Canyon",
        state: "Arizona",
        size_square_miles: 1902,
        date_founded: "02/26/1919",
        map_image: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/67/USA_Arizona_relief_location_map.svg/284px-USA_Arizona_relief_location_map.svg.png"
      }
      axios.post("/national_parks", newNationalParkParams).then(response => {
        console.log(response.date);
      })
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>New National Parks</h1>
    <div>
      <p>Name: <input type="text" /></p>
      <p>State: <input type="text" /></p>
      <p>Date Founded: <input type="text" /></p>
      <p>Size in Square Miles: <input type="text" /></p>
      <p>Map Image url: <input type="text" /></p>
      <button v-on:click="createNationalPark()">add a new park</button>


    </div>
    <h1>All National Parks</h1>
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