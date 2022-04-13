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
         lat: "40",
         long: "-74",
         appid: ""
      };
   },
   //get weather api data on mounted
   mounted() {
      axios
         .get(this.url + "lat=" + this.lat + "&lon=" + this.long + "&appid=" + this.appid)
         .then(response => (this.weatherData = response))
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
