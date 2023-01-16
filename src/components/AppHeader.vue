<script>
import { store } from '../store.js'
export default {
    data() {
        return {
            store,
        }
    },
}
</script>

<template>
    <div class="row">
        <div class="col-12">
            <label for="">Inserisci il film </label>
            <input type="text" v-model="store.searchText" >
            <button class="btn btn-success" @click="getApi(store.searchText)">cerca</button>
        </div>
        <div class="col-12">
            <ul>
                <li v-for="movie in store.moviesList" >
                    {{ movie.original_title  }}
                </li>
               
            </ul>
        </div>
    </div>
 
</template>

<style lang="scss" scoped>
</style>
