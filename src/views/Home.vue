<template>
    <v-container flat class="home">
        <v-row>
            <v-col>
                <v-pagination
                    v-model="page"
                    :length="length"
                    :circle="true"
                    :total-visible="totalVisible"
                ></v-pagination>
            </v-col>
        </v-row>

        <v-row>
            <template v-for="movie of movies">
                <v-col v-if="movie.poster_path" flat :key="movie.id">
                    <v-card v-if="movie.poster_path" flat link :to="'/movie/' + movie.id">
                        <v-img :src="imgPath + movie.poster_path"></v-img>
                    </v-card>
                </v-col>
            </template>
        </v-row>
    </v-container>
</template>

<script>
import axios from "axios";

export default {
    name: "home",
    data: () => ({
        imgPath: "https://image.tmdb.org/t/p/w300_and_h450_bestv2",
        movies: [],
        length: 50,
        page: 1,
        totalVisible: 10
    }),
    methods: {
        async loadMovies() {
            let res = await axios.get(
                // api_key should be at .env file, but for test task i've left it here.
                `https://api.themoviedb.org/3/discover/movie?api_key=d6628f0e1ca665f3395782a31b7006b6&page=${this.page}`
            );
            this.movies = res.data.results;
            this.page = res.data.page;
            this.length = res.data.total_pages;
        }
    },
    watch: {
        page: {
            handler: "loadMovies",
            immediate: true
        }
    }
};
</script>
