<template>
   <div id="main-wrapper" :class="temp > 85 ? 'summer' : temp > 65 ? 'spring' : temp > 35 ? 'fall' : 'winter'">
      <header id="weather-header">
         <h1>Your Weather App</h1>
      </header>
      <div id="weather-data">
         <strong class="temperature">
            {{  temp  }}
         </strong>
      </div>
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
* {
	margin: 0;
}
//for background image
#app, body, html {
	height: 100%;
}
#main-wrapper { 
   background-image: url('');
   background-size: cover;
   &.summer {
      background: url(assets/summerbeach.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
      @media (min-width: 768px) {
         background-size:50%;
      }
   }
   &.spring {
      background: url(assets/springflowers.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
      @media (min-width: 768px) {
         background-size:50%;
      }
   }
   &.fall {
      background: url(assets/fallleaves.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
      @media (min-width: 768px) {
         background-size:50%;
      }
   }
   &.winter {
      background: url(assets/wintersnow.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
      @media (min-width: 768px) {
         background-size:50%;
      }
   }
}

#weather-header {
	text-align: center;
	padding-top: 2%;
}

#weather-data {
   position: absolute;
   top: 50%;
   left: 50%;
   transform: translate(-50%, -50%);

   .temperature {
      font-size: 5em;
   }
}
</style>
