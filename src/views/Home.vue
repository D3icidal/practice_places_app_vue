<template>
  <div class="home">
    <h1>{{ message }}</h1><br>
    <p v-for='place in places'> {{place.name}}.  Located at {{place.address}}</p>
    <br>
    <p>New Place
      Name: <input type='text' v-model="newPlace.name"><br>
      Address: <input type='text' v-model="newPlace.address">
      <br>
      <button v-on:click="addPlace()">Submit Entry</button>
    </p>
  </div>
</template>

<style>
</style>

<script>
  var axios = require('axios');
  export default {
    data: function() {
      return {
        message: "aWeflcome to Vue.js!",
        places: [],
        newPlace: { name: "Empire State Building", address: "One Empire Stree"}
      };
    },
    created: function() {
      axios.get('http://localhost:3000/api/places').then(function(response) {
        console.log(response.data);
        this.places = response.data;
      }.bind(this));
    },

    methods: {
      addPlace: function() {
        var params = {
          name: this.newPlace.name,
          address: this.newPlace.address
        };
        axios.post('http://localhost:3000/api/places', params).then(function(response) {
          console.log('inside axios post');
          console.log(response.data);
          this.places.push(response.data);
        }.bind(this));
        console.log('adding new place - methods > addPlace > post axios');
        //this.place.push(this.newPlace); //adds the response from the axios-post to the vue array places
      }
    },
    computed: {}
  };
</script>

