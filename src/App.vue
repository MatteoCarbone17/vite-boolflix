<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import { store } from './store.js'
// import axios from 'axios'

export default {
  name: 'App',
  components: {
    AppMain,
    AppHeader,
  },

  data() {
    return {
      store,
    }
  },
  methods: {
    // getMovies(searchQuery) {
    //   axios.get(this.ApiUrl, {
    //     params: {
    //       api_key: this.apiKey,
    //       query: searchQuery,
    //     }
    //   })
    //     .then((response) => {
    //       this.store.moviesList = response.data.results;
    //       console.log(this.store.moviesList)

    //     });
    // },

  },

  created() {
   

  }

}

</script>


<template>
  <div>
    <AppHeader />
  </div>
  <div>
    <AppMain />
  </div>


</template>

<style lang="scss">
@use './components/style/general.scss' as *;
@use '../node_modules/bootstrap/scss/bootstrap.scss' as *;
</style>
