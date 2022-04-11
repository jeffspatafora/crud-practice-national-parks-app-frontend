<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      nationalParks: [],
      newNationalParkParams: {}
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
      axios.post("/national_parks", this.newNationalParkParams).then(response => {
        console.log("adding new park", response);
        this.nationalParks.push(response.data);
      })
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>New National Parks</h1>
    <div>
      <p>Name: <input type="text" v-model="newNationalParkParams.name" /></p>
      <p>State: <input type="text" v-model="newNationalParkParams.state" /></p>
      <p>Date Founded: <input type="text" v-model="newNationalParkParams.date_founded" /></p>
      <p>Size in Square Miles: <input type="text" v-model="newNationalParkParams.size_square_miles" /></p>
      <p>Map Image url: <input type="text" v-model="newNationalParkParams.map_image" /></p>
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