<template>
  <div class="home">
    <h1>{{ message }}</h1><br>
    <p v-for='place in places'> {{place.name}}.  Located at {{place.address}}</p>
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
        places: []
      };
    },
    created: function() {
      axios.get('http://localhost:3000/api/places').then(function(response) {
        console.log(response.data);
        this.places = response.data;
      }.bind(this));
    },

    methods: {},
    computed: {}
  };
</script>

