<template>
    <div>
      <v-app-bar app fixed color="yellow" dark>
        <v-spacer />
        <v-toolbar-title>
          <img
            class="mt-2 logo-pokedex"
            :src="require('../assets/logodigicard.png')"
          />
        </v-toolbar-title>  
        <v-spacer />
      </v-app-bar>
    </div>
  </template>
  
  <script>  
  export default {
    name: "navBar",
    data() {
      return {
      };
    },
  };
  </script>