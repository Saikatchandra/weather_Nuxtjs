<template>
  
  <v-app>
     <v-main>
       <v-toolbar color="indigo" dark>
         <!-- <v-toolbar-side-icon></v-toolbar-side-icon> -->
          <v-toolbar-title> 
            <n-link to="/">Nuxt Project</n-link>
            </v-toolbar-title>
           <v-spacer></v-spacer>
           <v-toolbar-items class="hidden-sm-and-down">
             <v-btn>
               <n-link to="/weather-app">Weather App</n-link>
             </v-btn>
             

           </v-toolbar-items>
       </v-toolbar>
        <nuxt />
     </v-main>
   </v-app>


</template>

<script>
export default {

}
</script>

<style scoped>

 a {
  text-decoration: none;
  color: white;
 }

</style>