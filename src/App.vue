<template>
  <div id="app">
    <!-- Homepagina -->
    <Homepage
     v-if="page == 'home'"
     @change-page="goToPage"
    />

    <!-- Game -->
    <Gamepage
     v-if="page == 'game'"
     @change-page="goToPage"
    />

    <!-- Ranking -->
    <Rankingpage
     v-if="page == 'ranking'"
     @change-page="goToPage"
    />

  </div>
</template>

<script>

//import of the whole styling for the app
import style from './scss/style.scss';

//import Pages
import Homepage from "./pages/Homepage.vue";
import Gamepage from "./pages/Gamepage.vue"
import Rankingpage from "./pages/Rankingpage.vue"

export default {
  name: 'App',
  components: {
    Homepage,
    Gamepage,
    Rankingpage
  },
  data(){
    return{
      page: "home"
    }
  },
  methods: {
    goToPage(page) {
      this.page = page;
    }
  }
}
</script>