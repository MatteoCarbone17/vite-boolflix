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
    getApi(searchQuery) {
      axios.get(this.ApiUrl, {
        params: {
          api_key: this.apiKey,
          query: searchQuery,
        }
      })
        .then((response) => {
          this.store.moviesList = response.data.results;
          console.log(this.store.moviesList)

        });
    },

  },

  created() {
    // this.getApi(searchQuery)

  }

}

</script>


<template>
  <!-- <div class="col-12">
            <label for="">Inserisci il film </label>
            <input type="text" v-model="store.searchText" >
            <button class="btn btn-success" @click="getApi(store.searchText)">cerca</button>
  </div> -->
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
