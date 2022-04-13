<template>
   <header id="weather-header">
      <h1>Your Weather App</h1>
   </header>
   <div>
      {{  weatherData  }}
   </div>
</template>

<script>
import axios from 'axios'


export default {
   name: 'App',
   data() {
      return {
         weatherData: null,
         url: "https://api.openweathermap.org/data/2.5/weather?",
         appid: "",
      };
   },
   computed: {
      getLat: function() {
         return navigator.geolocation.getCurrentPosition(function(position) {
            return position.coords.latitude;
         });
      },
      getLong: function() {
         return navigator.geolocation.getCurrentPosition(function(position) {
            return position.coords.longitude;
         });
      }
   },
   //get weather api data
   methods: {
      getWeatherData: function() {
         axios
            .get(this.url + "lat=" + this.getLat + "&lon=" + this.getLong + "&appid=" + this.appid)
            .then(response => (this.weatherData = response))
      }
   }
}
</script>

<style lang="scss">
html { 
   background: url(assets/summerbeach.jpg) no-repeat center center fixed; 
   background-size: cover;
   @media (min-width: 768px) {
      background-size:50%;
      background-color:seashell;
   }
}
</style>
