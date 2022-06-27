<template>
  <div id="app">
    <TheHeader />
    <main>
      <div class="container">
        <SortingComp />
        <div class="row row-cols-2 row-cols-sm-5">
          <div class="col card border-0" v-for="song in selected" :key="song.title">
            <SongCard :imgUrl="song.poster" :songTitle="song.title" :author="song.author" :year="song.year" />
          </div>
        </div>
      </div>
      <div class="loader" :class="{'d-none' : !loading}">
        <img src="./assets/disk.svg" alt="">
      </div>
    </main>
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue';
import SongCard from './components/SongCard.vue';
import axios from "axios";
import SortingComp from "./components/SortingComp.vue";
import { state } from "./components/store.js";

export default {
  name: 'App',
  data() {
    return {
      apiUrl: "https://flynn.boolean.careers/exercises/api/array/music",
      SongsList: state.SongsList,
      selected: state.selected,
      loading: false
    }
  },
  methods: {
    fetchSongList() {
      this.loading = true;
      axios.get(this.apiUrl).then((resp) => {
        state.SongsList = resp.data.response;
        state.selected = resp.data.response;
        this.loading = false
      })
    }
  },
  mounted() {
    this.fetchSongList();
  },
  components: {
    TheHeader,
    SongCard,
    SortingComp
}
}
</script>

<style lang="scss">
@import url('http://fonts.cdnfonts.com/css/gotham');

#app {
  font-family: 'Gotham', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

main {
  background: #1e2d3b;
  min-height: 100vh;

  .container {
    background: inherit;
    padding: 3rem 0;

    .row .col.card {
      background: inherit;
    }
  }
}

.loader{
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 100vh;
  background: rgba(0,0,0, 0.5);
  z-index: 11;

  img{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 200px;
    aspect-ratio: 1 / 1;
    animation: rotate 1s linear infinite;
  }
}

@keyframes rotate {
  from{
    transform: translate(-50%, -50%) rotate(0deg);
  }
  50%{
    transform: translate(-50%, -50%) rotate(180deg);
  }
  to{
    transform: translate(-50%, -50%) rotate(360deg);
  }
}
</style>
