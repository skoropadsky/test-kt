<template>
    <v-container flat class="home">
        <v-layout row wrap>
            <v-btn color="primary" dark text large to="/">
                <v-icon left>mdi-arrow-left</v-icon> Back
            </v-btn>
        </v-layout>
        <v-layout row wrap justify-center v-if="isLoaded">
            <v-flex col xs12 md2>
                <v-img :src="imgPath + movie.poster_path"></v-img>
            </v-flex>
            <v-flex col xs12 md6 text-left>
                <h2 class="display-2 mb-10">{{ movie.title }}</h2>
                <v-simple-table>
                    <template v-slot:default>
                        <tbody>
                            <tr>
                                <td>Описание:</td>
                                <td>{{ movie.overview }}</td>
                            </tr>
                            <tr>
                                <td>IMBD:</td>
                                <td>{{ movie.imdb_id }}</td>
                            </tr>
                            <tr>
                                <td>Релиз:</td>
                                <td>{{ movie.release_date }}</td>
                            </tr>
                            <tr>
                                <td>Бюджет:</td>
                                <td>{{ movie.budget }}</td>
                            </tr>
                        </tbody>
                    </template>
                </v-simple-table>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
import axios from "axios";

export default {
    name: "home",
    data: () => ({
        movie: {},
        imgPath: "https://image.tmdb.org/t/p/w300_and_h450_bestv2",
        isLoaded: false
    }),
    async beforeMount() {
        let res = await axios.get(
            // api_key should be at .env file, but for test task i've left it here.
            `https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=d6628f0e1ca665f3395782a31b7006b6`
        );
        this.movie = res.data;
        this.isLoaded = true;
    }
};
</script>
