<template>
  <v-app>
    <NavBar>
    <v-main>
      <router-view/>
    </v-main>
    </NavBar>
  </v-app>
</template>

<script>
import NavBar from "./components/NavBar.vue"
export default {
  name: 'App',
  components:{
    NavBar
  },

  data: () => ({
    //
  }),
};
</script>
