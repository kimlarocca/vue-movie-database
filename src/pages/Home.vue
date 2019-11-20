<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="grid">
      <div class="cell"
           v-for="(movie, index) in movies"
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
    name: 'HelloWorld',
    components: {
      'movie-card': MovieCard
    },
    data () {
      return {
        msg: 'Movie Database App',
        movies: null
      }
    },
    mounted () {
      axios
        .get('https://api.themoviedb.org/3/movie/popular?api_key=83d3415a37a96ef11c1ae22b98c556da&language=en-US&page=1')
        .then(response => (this.movies = response.data.results))
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  a,
  a:visited,
  a:active {
    cursor: pointer;
    color: purple;
  }

  .grid {
    display: flex;
    flex-wrap: wrap;
    margin: auto;
    justify-content: center;
  }

  .cell {
    margin: 1rem;
  }
</style>
