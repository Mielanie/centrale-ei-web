<template>
  <div>
    <router-link :to="{path: '/' + movie.id}"><div
      class="test"
      :style="`
        background-image: url(${f(movie.poster_path)});
      `"
    >
      <div class="inside">
        <h5>{{ movie.title || movie.name }}</h5>
        {{ g(movie.overview) }}
        <br /><br />
        {{ i(movie.vote_average) }}
      </div>
    </div>
    </router-link>
  </div>
</template>

<script>
export default {
  name: "Movie",
  props: {
    movie: Object,
  },
  methods: {
    f: function (url) {
      return "https://image.tmdb.org/t/p/w200" + url;
    },
    g: function (texte) {
      if (texte.length < 200) {
        return texte;
      } else {
        return texte.slice(0, 200) + "...";
      }
    },
    i: function (vote) {
      let answer = "";
      for (let i = 0; i < Math.trunc(vote / 2); i++) {
        answer += "⭐️";
      }
      return answer;
    },
  },
};
</script>
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
  margin: 5px;
}
.test:hover {
  width: 200px;
}

.inside {
  background: black;
  opacity: 0;
  height: 100%;
  padding: 5px;
  overflow: hidden;
  text-overflow: ellipsis;
  transform: translateY(1em);
}

.test:hover .inside {
  background: black;
  opacity: 0.7;
  transition: 0.4s;
  transform: translateY(0em);
}
</style>
