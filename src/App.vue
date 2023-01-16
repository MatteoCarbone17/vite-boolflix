<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import { store } from './store.js'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    AppMain,
    AppHeader,
  },

  data() {
    return {
      store,
      apiKey:'d375deb50bb5135ee140c55f9476e44c',
      ApiUrl: 'https://api.themoviedb.org/3/search/movie?'
    }
  },
  methods: {
    getApi() {
      axios.get(this.ApiUrl, {
        params: {
          api_key: this.apiKey,
          query: 'harry',
        }
      })
        .then((response) => {
          this.store.moviesList = response.data.results;
          console.log(this.store.moviesList)

        });
    },

  },

  created() {
    this.getApi()

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
