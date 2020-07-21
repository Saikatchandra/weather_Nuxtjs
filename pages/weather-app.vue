<template>
    
 <v-container>
     <h2 class="text-center">Weather app</h2>
      <v-col cols="12">
          <v-card color="blue-grey darken-2" dark>
              <v-card-text>
                  <v-layout justify-center>
                  <v-col class="text-center">
                      <h4>Temperature</h4>
                      <h2> {{weather.name}} </h2>
                      <img :src="icon" alt="weather_icon">
                      <p>
                          <span> {{ temp() }} &deg;C  </span>
                          <span class="caption ml-4"> {{weather.weather[0].description}} </span>
                      </p>
                  </v-col>
                   <v-col class="text-center">
                      <h4>Wind & Pressure</h4>
                      <h3 class="headline"> Wind: {{weather.wind.speed}} m/s ({{weather.wind.deg}}) &deg;C   </h3>
                      <h3 class="headline mt-2"> Humidity: {{weather.main.humidity}}%   </h3>
                     <h3 class="headline mt-2"> Pressure: {{weather.main.pressure}}  hpa   </h3>
                  </v-col>
                   <v-col class="text-center">
                      <h4>Other</h4>
                      <h3 class="headline mt-2"> Max Temp: {{Math.round(weather.main.temp_max -273)}} &deg;C    </h3>
                      <h3 class="headline mt-2"> Min Temp: {{Math.round(weather.main.temp_min -273)}} &deg;C    </h3>
                  </v-col>
                  </v-layout>
                  
              </v-card-text>
          </v-card>
      </v-col>
    <v-col cols="12" class="mt-4">
        <v-form @submit.prevent="getWeatherInfo">
            <v-text-field v-model="city"
            label="Enter city here....."
            solo
          ></v-text-field>
        </v-form>
          
        </v-col>

  </v-container>

</template>    
<script>
export default {

    data(){
        return{
            city: "",
            // weather: {},

        }
    },

    created(){
       this.getWeatherInfo()
    },
  
//This is for server side rendering (SSR)
    asyncData ({ params,$axios }) {
    return $axios.$get(`https://api.openweathermap.org/data/2.5/weather?q=london&appid=${process.env.weatherAppId}`)
      .then((res) => {
        return { weather: res }
      })
  },

    computed:{
        icon(){
            return this.weather.weather 
            ? `https://openweathermap.org/img/w/${this.weather.weather[0].icon}.png`
            : ''
        }
    },

    methods:{
        getWeatherInfo(){
             this.$axios.$get(
            `https://api.openweathermap.org/data/2.5/weather?q=${this.city
            }&appid=${process.env.weatherAppId}`
        ).then(res => (this.weather = res))
        },
        
        temp(){
            return Math.round(this.weather.main.temp - 273)
        }
    }
}
</script>
<style scoped>

</style>