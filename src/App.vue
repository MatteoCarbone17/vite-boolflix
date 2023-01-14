<script>
import { store } from '../src/store.js'
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      return:
      store,
      ApiUrl: 'https://api.themoviedb.org/3/movie/550?api_key=d375deb50bb5135ee140c55f9476e44c'
    }
  },
  methods: {
    getApi() {
      axios.get(this.ApiUrl, {

      })
        .then((response) => {

        console.log(response.data)
          // console.log(this.store.data)

        });
    },

  },

created(){
     this.getApi()}

}

</script>


<template>

</template>

<style lang="scss">
@use './components/style/general.scss' as *;
@use '../node_modules/bootstrap/scss/bootstrap.scss' as *;
</style>
