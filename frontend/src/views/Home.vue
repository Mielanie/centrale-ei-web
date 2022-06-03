<template>
  <div class="home">
    <br /><br /><br />
    <img class="logo" alt="Vue logo" src="../assets/morbiustv.png" />
    <h1>MorbiusTV+ {{ movieName }} {{ 1 }}</h1>
    <p>Recommande tous les films possible, sauf Morbius.</p>
    <p>Message is: {{ movieName }}</p>
    <p>{{ movies.length }}</p>
    <li v-for="item in movies" :key="item">
      <!-- <img :src="`https://image.tmdb.org/t/p/w200${item.poster_path}`" /> -->
      <div
        class="test"
        :style="`
        background-image: url(${f(item.poster_path)});
      `"
        @touch="darken()"
      >
        {{ item.title || item.name }}
      </div>
    </li>
    <input v-model="movieName" placeholder="edit me" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data: function () {
    return { movieName: "h", movies: [{ id: "5" }] };
  },
  methods: {
    f: function (url) {
      return "https://image.tmdb.org/t/p/w200" + url;
    },
    darken: function () {},
  },
  created() {
    axios
      .get(
        `https://api.themoviedb.org/3/movie/popular?api_key=522d421671cf75c2cba341597d86403a`
      )
      .then((response) => {
        // Do something if call succeeded
        this.movies = response.data.results;
        console.log(response.data.results);
      })
      .catch((error) => {
        // Do something if call failed
        console.log(error);
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
