<script setup>
/* eslint-disable */
import {
  ref
} from 'vue'

let search = ref("");
let movies = ref([]);

async function findMovies() {
  await fetch(
    `https://api.themoviedb.org/3/search/movie?api_key=ed82f4c18f2964e75117c2dc65e2161d&query=${search.value}`
  ).then(async (res) => {
    let fetchMovies = await res.json()
    movies.value = fetchMovies.results
    console.log(movies.value)
  });

};

</script>

<template>
<main>
    <div :class="{'search-container': !movies.length}" class="always-search-container">
      <img src="/assets/icons/logo.png" alt="logo">
      <input type="text" v-model="search" class="find-input" @input="findMovies()" placeholder="Entrez le titre d'un film">
    </div>
    
 
    <div class="result-container">
      <ul class="result-list">
        <li v-for="movie in movies">
          <h2>{{movie.original_title}}</h2>
          <div class="card-content">
            <img :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path">
            <div class="infos">
              <p style="height: 45px; overflow:hidden;">{{movie.overview}}</p>
              <p>Popularité : {{movie.popularity}}</p>
            </div>
          </div>
        </li>
      </ul>
    </div>

  </main>
</template>

<style lang="scss">
#app {
  margin-right: 80px;
  margin-left: 80px;
}

.search-container {
  margin-top: 400px;
}

.always-search-container {

  img {
    width: 100px;
  }

  .find-input {
    display: block;
    width: 80%;
    padding: 8px 16px;
    line-height: 25px;
    font-size: 14px;
    font-weight: 500;
    font-family: inherit;
    border-radius: 6px;
    margin-right: auto;
    margin-left: auto;
  }
}

.result-container {
  max-width: 100%;
  display: flex;
  justify-content: center;
  .result-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 0;
    gap: 40px;
    li {
      flex: 1 1 210px;

      img {
        width: 200px;
      }
    }
  }
}
</style>