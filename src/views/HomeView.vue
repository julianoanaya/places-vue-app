<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      places: [],
      newPlacesParams: {},
      editPlaceParams: {},
      currentPlace: {},
    };
  },
  created: function () {
    this.indexPlaces();
  },
  methods: {
    indexPlaces: function () {
      axios.get("/places").then((response) => {
        console.log("places index", response);
        this.places = response.data;
      });
    },
    createPlace: function () {
      console.log("Creating place...");

      var params = this.newPlaceParams;

      axios
        .post("http://localhost:3000/places.json", params)
        .then((response) => {
          console.log("Created Place", response.data);
          this.place.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showPlace: function (place) {
      console.log("info is shown", place);
      this.currentPlace = place;
      this.editPlaceParams = place;
      document.querySelector("#place-details").showModal();
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>All places</h1>
    <h2>New Place</h2>
    <div>
      Name:
      <input type="text" v-model="newPlacesParams.name" />
    </div>
    <div>
      Price:
      <input type="text" v-model="newPlacesParams.address" />
    </div>
    <button v-on:click="createProduct()">Create Product</button>
    <div v-for="place in places" v-bind:key="place.id">
      <h2>{{ place.name }}</h2>
      <h2>{{ place.address }}</h2>
    </div>
    <dialog id="place-details">
      <form method="dialog">
        <h2>Place info</h2>
        <p>Name: {{ currentPlace.name }}</p>
        <p>Address: {{ currentPlace.address }}</p>
      </form>
    </dialog>
  </div>
</template>

<style></style>
