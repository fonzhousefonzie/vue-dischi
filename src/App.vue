<template>
  <div id="app">
    <TheHeader />
    <main>
      <div class="container">
        <h4 class="text-light">Filters:</h4>
        <div class="filters d-flex justify-content-center gap-3 pb-3">
          <div class="dropdown">
            <button class="btn btn-success dropdown-toggle" type="button" id="dropdownMenuButton1"
              data-bs-toggle="dropdown" aria-expanded="false">
              Genre
            </button>
            <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
              <li><a class="dropdown-item" href="#" @click.prevent="resetList()">All</a></li>
              <li><a class="dropdown-item" href="#" v-for="genre in genreList" :key="genre" @click.prevent="selectGenre(genre)">{{ genre }}</a></li>
            </ul>
          </div>
          <div class="dropdown">
            <button class="btn btn-success dropdown-toggle" type="button" id="dropdownMenuButton1"
              data-bs-toggle="dropdown" aria-expanded="false">
              Author
            </button>
            <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
              <li><a class="dropdown-item" href="#" @click.prevent="resetList()">All</a></li>
              <li><a class="dropdown-item" href="#" v-for="author in authorsList" :key="author" @click.prevent="selectAuthor(author)">{{ author }}</a></li>
            </ul>
          </div>
        </div>
        <div class="row row-cols-2 row-cols-sm-5">
          <div class="col card border-0" v-for="song in selected" :key="song.title">
            <SongCard :imgUrl="song.poster" :songTitle="song.title" :author="song.author" :year="song.year" />
          </div>
        </div>
      </div>
      <div class="loader" :class="loading">
        <img src="./assets/disk.svg" alt="">
      </div>
    </main>
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue';
import SongCard from './components/SongCard.vue';


import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
      apiUrl: "https://flynn.boolean.careers/exercises/api/array/music",
      SongsList: [],
      selected: [],
      genreList: [],
      authorsList: []
    }
  },
  computed:{
    loading(){
      if(this.selected !== null){
        return 'd-none'
      } else {
        return 'd-block'
      }
    }
  },
  methods: {
    fetchSongList() {
      axios.get(this.apiUrl).then((resp) => {
        // Songs
        this.SongsList = resp.data.response;
        this.selected = resp.data.response;
        // Genres
        for (let i=0; i < this.SongsList.length; i++){
          if(!this.genreList.includes(this.SongsList[i].genre)){
            this.genreList.push(this.SongsList[i].genre)
          }
        }
        for (let i=0; i < this.SongsList.length; i++){
          if(!this.authorsList.includes(this.SongsList[i].author)){
            this.authorsList.push(this.SongsList[i].author)
          }
        }
      })
    },
    selectGenre(genre){
      this.selected = [];
      for (let i=0; i<this.SongsList.length; i++){
        if(this.SongsList[i].genre === genre){
          this.selected.push(this.SongsList[i]);
        }
      }
    },
    selectAuthor(author){
      this.selected = [];
      for (let i=0; i<this.SongsList.length; i++){
        if(this.SongsList[i].author === author){
          this.selected.push(this.SongsList[i]);
        }
      }
    },
    resetList(){
      this.selected = this.SongsList;
    }
  },
  mounted() {
    this.fetchSongList();
  },
  components: {
    TheHeader,
    SongCard
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
