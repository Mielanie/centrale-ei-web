<template>
  <div class="home">
    <br /><br /><br />
    <img class="logo" alt="Vue logo" src="../assets/morbiustv.png" />
    <h1>MorbiusTV+ {{ movieName }} {{ 1 }}</h1>
    <p>Recommande tous les films possible, sauf Morbius.</p>
    <p>Message is: {{ movieName }}</p>
    <p>{{ movies.length }}</p>
    <li v-for="item in movies" :key="item.id">
      <Movie :movie="item" />
    </li>
    <br />
    <br />
    <input v-model="movieName" placeholder="edit me" />
  </div>
</template>

<script>
import axios from "axios";
import Movie from "@/components/Movie.vue";

export default {
  name: "Home",
  components: {
    Movie,
  },
  data: function () {
    return { movieName: "h", movies: [{ id: "5" }] };
  },
  methods: {
    f: function (url) {
      return "https://image.tmdb.org/t/p/w200" + url;
    },
  },
  created() {
    axios
      .get(
        `https://api.themoviedb.org/3/movie/popular?api_key=522d421671cf75c2cba341597d86403a`
      )
      .then((response) => {
        // Do something if call succeeded
        this.movies = response.data.results;
      })
      .catch((error) => {
        // Do something if call failed
      });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.logo {
  width: 300px;
}
.home {
  text-align: center;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.test {
  height: 300px;
  width: 200px;
}
</style>
