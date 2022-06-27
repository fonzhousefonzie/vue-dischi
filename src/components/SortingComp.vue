<template>
    <div>
        <h4 class="text-light">Sort by:</h4>
        <div class="filters d-flex justify-content-center gap-3 pb-3">
            <div class="dropdown">
                <button class="btn btn-success dropdown-toggle" type="button" id="dropdownMenuButton1"
                    data-bs-toggle="dropdown" aria-expanded="false">
                    Genre
                </button>
                <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                    <li><a class="dropdown-item" href="#" @click.prevent="resetList()">All</a></li>
                    <li><a class="dropdown-item" href="#" v-for="genre in findGenres" :key="genre"
                            @click.prevent="selectGenre(genre)">{{ genre }}</a></li>
                </ul>
            </div>
            <div class="dropdown">
                <button class="btn btn-success dropdown-toggle" type="button" id="dropdownMenuButton1"
                    data-bs-toggle="dropdown" aria-expanded="false">
                    Author
                </button>
                <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                    <li><a class="dropdown-item" href="#" @click.prevent="resetList()">All</a></li>
                    <li><a class="dropdown-item" href="#" v-for="author in findAuthors" :key="author"
                            @click.prevent="selectAuthor(author)">{{ author }}</a></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import { state } from "./store.js"

export default {
    methods: {
        selectGenre(genre) {
            state.selected = [];
            for (let i = 0; i < state.SongsList.length; i++) {
                if (state.SongsList[i].genre === genre) {
                    state.selected.push(state.SongsList[i]);
                }
            }
        },
        selectAuthor(author) {
            state.selected = [];
            for (let i = 0; i < state.SongsList.length; i++) {
                if (state.SongsList[i].author === author) {
                    state.selected.push(state.SongsList[i]);
                }
            }
        },
        resetList() {
            state.selected = state.SongsList;
        }
    },
    computed: {
        findGenres() {
            const genreList = [];
            for (let i = 0; i < state.SongsList.length; i++) {
                if (!genreList.includes(state.SongsList[i].genre)) {
                    genreList.push(state.SongsList[i].genre)
                }
            }
            return genreList;
        },
        findAuthors() {
            const authorsList = [];
            for (let i = 0; i < state.SongsList.length; i++) {
                if (!authorsList.includes(state.SongsList[i].author)) {
                authorsList.push(state.SongsList[i].author)
                }
            }
            return authorsList;
        }
    }
}
</script>