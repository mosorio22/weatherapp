<template>
   <header id="weather-header">
      <h1>Your Weather App</h1>
   </header>
</template>

<script>

export default {
   name: 'App',
   data() {
      return {
         url: "https://api.openweathermap.org/data/2.5/weather?",
         lat: "",
         long: "",
         api_key: ""
      };
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
