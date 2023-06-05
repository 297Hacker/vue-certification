<script setup>
import {reactive, ref} from 'vue';
import { items } from "./movies.json";
import Star from "./component/Star.vue";
/*
 This is an Icon that you can use to represent the stars if you like
 otherwise you could just use a simple ⭐️ emoji, or * character.
*/

const movies = reactive(items);
const customRating = ref(0);
const movie = ref(false);
const movieContent = reactive({
  id: movies.length + 1,
  name: null,
  description: null,
  image: null,
  genres: [],
  rating: 0,
  customRating: null,
  inTheater: false
})

const addRating = function(){
  for(let i in movies){
    movies[i].customRating = customRating.value;
  }
}

const resetMovie = function(){
  movieContent.id = null;
  movieContent.name = null;
  movieContent.description = null;
  movieContent.image = null;
  movieContent.genres = [];
  movieContent.rating = 0;
  movieContent.customRating = 0;
  movieContent.inTheater = false;
}

const showMovie = function(){
  movie.value = true;
}

const addMovie = function(){
  movies.push(movieContent);
  movie.value = false;
  console.log(movies);
  if(!movie){
    resetMovie();
  }
}

addRating();
</script>

<template>
  <section>
  <h1>Movie app</h1>
    <div v-for="item in movies" class="movie">
      <Star :rating="item.customRating"></Star>
      <img class="movie-img" :src="item.image"/>
    <h1>{{item.name}}</h1>
      {{item.description}}
        <template v-for="element in item.genres">
          <b>{{ element }}</b>
        </template>
      <tr></tr>
      Movie Rating: {{ item.rating }}
      <tr></tr>
      <button class="rating-btn" @click="item.customRating < 5 ? item.customRating++ : null">+</button>
      <button class="rating-btn" @click="item.customRating > 0 ? item.customRating-- : null">-</button>
      Your Rating: {{ item.customRating }}
      <template v-for="j in item.customRating">
        ⭐️
      </template>
    </div>
    <button :class="movie ? 'disable' : 'enable'" @click="showMovie()">Add movie</button>
    <form :class="movie ? 'show' : 'hide'">
      <label>Title:</label>
      <input v-model="movieContent.name" />
      <label>Description:</label>
      <textarea v-model="movieContent.description" />
      <label>Genre:</label>
      <input v-model="movieContent.genres" />
      <label>Image:</label>
      <input v-model="movieContent.image" />
      <button class="add" @click.prevent="addMovie()">Add</button>
    </form>
  </section>
</template>
<style>
.movie{
  margin-top: 100px;
  width: 20%; 
  float: left;
  position: relative;
}
b{
  margin-right: 5px;
}
.movie-img {
width: 150px;
}
.rating-btn{
  padding: 10px;
  background-color: aqua;
  margin-right: 5px;
  border-radius: 5px;
}

form.hide {
  display: none;
}

form.show {
  display: block;
}
</style>