<script>
import { store } from '../store.js'
import axios from 'axios'
// import LangFlag from 'vue-lang-code-flags'
// import vue3starRatings from "vue3-star-ratings";


export default {
    components: {
        // LangFlag,
        // vue3starRatings,
    },
    data() {
        return {
            store,
            apiKey: 'd375deb50bb5135ee140c55f9476e44c',
            ApiUrl: 'https://api.themoviedb.org/3/search/multi?',
            ApiUrlImagePath: 'https://image.tmdb.org/t/p/w342/',
            iconFlagList: ['en','it', 'es','fr','ch', 'us' ],
            hover: false,
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
        getRating(rating) {
            rating = Math.floor(rating / 2);
            return rating;
        },
        getIconPath: function(imgPath) {
        return new URL(`../assets/img/flag_icon/${imgPath}.png`, import.meta.url).href;
    }

    },
}
</script>

<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-6 bg-dark p-3">
                <h1 class="text-danger">
                    BOOLFLIX
                </h1>
            </div>
            <div class="col-6 bg-dark p-3 d-flex align-items-center justify-content-end">
                <label class="me-2" for="">Inserisci il nome del film:</label>
                <input class="me-2" type="text" v-model="store.searchText">
                <button class="btn btn-primary ms-2" @click="getMovies(store.searchText)">Avvia ricerca</button>
            </div>
            <div class="col-12 mt-2">
                <ul class="d-flex flex-wrap" >
                    <!-- "$data[myCondition ? 'name' : 'title']" ternario esempio -->
                    <li v-for="movie in store.moviesList">
                        <img v-if="(!hover)" @mouseover="(hover = true)" @mouseleave="(hover = false)"  :src="getImagePath(movie.backdrop_path)" alt="" srcset="">
                        <div v-else class="bg-black text-light info-container" >
                            <h6>
                                Titolo Originale: {{ movie.original_title }} {{ movie.original_name }}
                                <br>
                                Titolo: {{ movie.title }} {{ movie.name }}
                            </h6>
                            <p>
                                 Overview:  {{ movie.overview }}
                            </p>
                            <img :src="getIconPath(movie.original_language)"  v-if="iconFlagList.includes(movie.original_language)"  alt="" srcset="">
                            <!-- <lang-flag v-if="(movie.original_language)" :iso="movie.original_language" /> -->
                            <div v-else>
                                <span><i class="fa-solid fa-globe"></i> Language not found </span>
                            </div>
                            <p class="p-rating">
                                <!-- <vue3starRatings v-model="movie.vote_average" /> -->
                                Voto: {{ getRating(movie.vote_average) }}/5
                            </p>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>

</template>

<style lang="scss" scoped>
ul{
    margin-bottom: 2rem;
}

li {
    list-style-type: none;
    width: calc(100% / 7 );
    img{
        margin-bottom: 1rem;
    }
}
div.info-container{
   margin: 1rem;
   height: 98%;
   padding: 1rem;

}


</style>
