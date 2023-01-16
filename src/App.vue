<script>
import AppHeader from './components/AppHeader.vue'
import AppMain from './components/AppMain.vue'
import { store } from './store.js'

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
