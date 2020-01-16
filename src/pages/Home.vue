<template>
    <div :class="darkTheme ? 'dark' : 'light'">
        <h1>{{ msg }}</h1>
        <p @click="darkTheme = !darkTheme">toggle light/dark theme</p>
        <input type="text" placeholder="search movies" v-model="keyword">
        <p v-if="filteredMovies.length === 0">no results found. <a @click="keyword=null">clear filters</a></p>
        <div class="grid">
            <div class="cell"
                 v-for="(movie, index) in filteredMovies"
                 :key="index">
                <movie-card
                        :title="movie.title"
                        :image="movie.backdrop_path"
                        :overview="movie.overview"
                >
                </movie-card>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    import MovieCard from '../components/MovieCard'

    export default {
        name: 'Home',
        components: {
            'movie-card': MovieCard
        },
        data () {
            return {
                msg: 'Movie Database App',
                movies: null,
                keyword: null,
                darkTheme: false
            }
        },
        mounted () {
            axios
                .get('https://api.themoviedb.org/3/movie/popular?api_key=83d3415a37a96ef11c1ae22b98c556da&language=en-US&page=1')
                .then(response => (this.movies = response.data.results))
        },
        computed: {
            filteredMovies () {
                if (this.keyword) {
                    return this.movies.filter(movie => {
                        return movie.title.toLowerCase().includes(this.keyword.toLowerCase());
                    })
                } else {
                    return this.movies;
                }
            }
        }
    }
</script>

<style lang="scss">
    body {
        margin: 0;
    }

    h1, h2 {
        font-weight: normal;
        margin: 0 0 1rem 0;
    }

    a,
    a:visited,
    a:active {
        cursor: pointer;
        color: purple;
    }

    input {
        padding: 10px;
        margin-bottom: 1rem;
        width: 200px;
        font-size: 1rem;
        color: #333;
    }

    .grid {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;

        .cell {
            margin: 1rem;
        }
    }
.light {
    transition: 500ms;
}
    .dark {
        transition: 500ms;
        background: #333;
        color: white;
    }
</style>
