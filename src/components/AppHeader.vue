<script>
import { store } from '../store.js'
import axios from 'axios'
export default {
    data() {
        return {
            store,
            apiKey: 'd375deb50bb5135ee140c55f9476e44c',
            ApiUrl: 'https://api.themoviedb.org/3/search/movie?'
        }
    },
    methods: {
        getMovies(searchQuery) {
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
}
</script>

<template>
    <div class="row">
        <div class="col-12">
            <label for="">Inserisci il nome del film</label>
            <input type="text" v-model="store.searchText">
            <button class="btn btn-success" @click="getMovies(store.searchText)">Avvia ricerca</button>
        </div>
        <div class="col-12">
            <ul>
                <li v-for="movie in store.moviesList">
                   <h5>
                    {{ movie.original_title }}
                   </h5>
                   <h6>
                    {{  movie.title }}
                   </h6>
                   <p>
                     {{ movie.original_language }}
                     Rating: {{ movie.vote_average  }}
                   </p>
                </li>

            </ul>
        </div>
    </div>

</template>

<style lang="scss" scoped>

</style>
