<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import { store } from './store.js'
import axios from 'axios'

export default {
  name: 'App',
  components :{
        AppMain,
        AppHeader,
    },
    
  data() {
    return {
      store,
      ApiUrl: 'https://api.themoviedb.org/3/movie/550?api_key=d375deb50bb5135ee140c55f9476e44c'
    }
  },
  methods: {
    getApi() {
      axios.get(this.ApiUrl, {

      })
      .then((response) => {
        this.store.dataStore = response.data 
        console.log(this.store.dataStore)

        });
    },

  },

created(){
     this.getApi()
    
    }

}

</script>


<template>

  <AppHeader />
  <AppMain />
  
  <p>{{ store.data }}</p>

</template>

<style lang="scss">
@use './components/style/general.scss' as *;
@use '../node_modules/bootstrap/scss/bootstrap.scss' as *;
</style>
