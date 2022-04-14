<template>
   <header id="weather-header">
      <h1>Your Weather App</h1>
   </header>
   <div>
      {{  temp  }}
   </div>
</template>

<script>
import axios from 'axios'


export default {
   name: 'App',
   data() {
      return {
         temp: null,
         url: "https://api.openweathermap.org/data/2.5/weather?",
         appid: ""
      };
   },
   //get weather api data
   mounted() {
      //var to hold component data scope
      let that = this;
      //get lat and long and pass into weather api
      //save data in Farenheit (from Kelvin)
      navigator.geolocation.getCurrentPosition(function(position) {
         axios
         .get(that.url + "lat=" + position.coords.latitude + "&lon=" + position.coords.longitude + "&appid=" + that.appid)
         .then(response => (that.temp = ((response.data.main.temp - 273.15) * 9/5 + 32).toFixed(1)))
      });
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
