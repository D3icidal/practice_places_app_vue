<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p v-for='place in places'> {{places.name}} </p>
  </div>
</template>

<style>
</style>

<script>
  var axios = require('axios');
  export default {
    data: function() {
      return {
        message: "Weflcome to Vue.js!",
        places: []
      };
    },
    created: function() {
      axios.get('http://localhost:3000/api/places').then(function(response) {
        console.log(response.data);
        this.recipe = response.data;
      }.bind(this));
    },

    methods: {},
    computed: {}
  };
</script>

