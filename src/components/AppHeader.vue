<script>
import { store } from '../store.js'
import axios from 'axios'
import LangFlag from 'vue-lang-code-flags'


export default {
    components: {
        LangFlag,
  },
    data() {
        return {
            store,
            apiKey: 'd375deb50bb5135ee140c55f9476e44c',
            ApiUrl: 'https://api.themoviedb.org/3/search/multi?',
            ApiUrlImagePath: 'https://image.tmdb.org/t/p/w342/'
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
        getImagePath(imgPath) {
            return (this.ApiUrlImagePath + imgPath);
        },
        getRating(rating){
           rating = Math.floor(rating / 2);
           return rating;
        }

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
                        {{ movie.original_title }} {{ movie.original_name }}
                    </h5>
                    <h6>
                        {{ movie.title }} {{ movie.name }}
                    </h6>
                    <p>
                       <lang-flag v-if="(movie.original_language)" :iso="movie.original_language" />
                       <div v-else >
                        <span><i class="fa-solid fa-globe"></i> Language not found </span>
                       </div>
                        Rating: {{ getRating(movie.vote_average) }}
                    </p>
                    <img :src="getImagePath(movie.backdrop_path)" alt="" srcset="">
                </li>

            </ul>
        </div>
    </div>

</template>

<style lang="scss" scoped>

</style>
