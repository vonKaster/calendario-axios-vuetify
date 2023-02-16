<template>
  <v-app>
    <navBar></navBar>
    <v-main>
      <v-container>
        <router-view />

        <v-dialog v-model="loading.estado" hide-overlay persistent width="300">
          <v-card color="primary" dark>
            <v-card-text :color="loading.color" dark>
              {{ loading.titulo }}
              <v-progress-linear
                indeterminate
                color="white"
                class="mb-0"
              ></v-progress-linear>
            </v-card-text>
          </v-card>
        </v-dialog>
      </v-container>
    </v-main>
    <Footer></Footer>
  </v-app>
</template>

<script>
import { mapState } from 'vuex';
import navBar from './components/navBar.vue';
import Footer from './components/Footer.vue';

export default {
  name: "App",
  components: {
        navBar,
        Footer
    },

  data: () => ({
    //
  }),
  computed:{
    ...mapState(['loading'])
  }
};
</script>
