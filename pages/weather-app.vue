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
            city: "london",
            weather: {},
        }
    },

    created(){
       this.getWeatherInfo()
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
            }&appid=3da2c310fe5e76482c133afd055b3930`
        ).then(res => (this.weather = res))
        }
    }
}
</script>
<style scoped>

</style>