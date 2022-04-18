<template>
   <div id="main-wrapper" :class="getTemp > 85 ? 'summer' : getTemp > 65 ? 'spring' : getTemp > 35 ? 'fall' : getTemp > - 300 ? 'winter' : 'noTemp'">
      <header id="weather-header">
         <h1>Your Weather App</h1>
      </header>
      <div id="weather-data">
         <strong class="temperature">
            {{  getTemp  }}&#176;
         </strong>
         <p class="location">
            {{  getLocation  }}
         </p>
      </div>
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
         appid: ""
      };
   },
   computed: {
      //get temp in Farenheit (from Kelvin)
      getTemp() {
         if (this.weatherData !== null) {
            return ((this.weatherData.data.main.temp - 273.15) * 9/5 + 32).toFixed(1);
         }
         else {
            return "?";
         }
      },
      //get location
      getLocation() {
         if (this.weatherData !== null) {
            return this.weatherData.data.name;
         }
         else {
            return "";
         }
      }
   },
   //get weather api data
   mounted() {
      //var to hold component data scope
      let that = this;
      //get lat and long and pass into weather api
      navigator.geolocation.getCurrentPosition(function(position) {
         axios
         .get(that.url + "lat=" + position.coords.latitude + "&lon=" + position.coords.longitude + "&appid=" + that.appid)
         .then(response => (that.weatherData = response))
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
   background-size: cover;
   &.summer {
      background: url(assets/summerbeach.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
   }
   &.spring {
      background: url(assets/springflowers.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
   }
   &.fall {
      background: url(assets/fallleaves.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
   }
   &.winter {
      background: url(assets/wintersnow.jpg) no-repeat center center fixed;
      background-size: cover;
      height: 100%;
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

   .location {
      font-size: 2em;
      text-align: center;
   }
}
</style>
