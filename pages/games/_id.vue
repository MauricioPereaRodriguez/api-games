<template>
  <div>
    <b-container class="mt-3">
      <b-row>
        <b-col cols="3">
          <img :src="game.cover.url.replace('t_thumb', 't_cover_big')" alt="portada">
        </b-col>
        <b-col cols="9">
          <b-card
          :title="game.name"
          class="mb-2">
            <b v-for="(consola, index) in game.platforms" :key="index">{{consola.name}}</b>
            <p class="card-text">{{game.summary}}</p>
            <div v-if="game.total_rating != null" >
              <p>Calificación: {{ Math.round(game.total_rating) }}</p>
            </div>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
    <b-container class="mt-3">
      <b-carousel
        id="carousel"
        style="text-shadow: 1px 1px 2px #333;"
        controls
        indicators
        :interval="4000"
        img-width="1024"
        img-height="480"
        v-model="slide"
        @sliding-start="onSlideStart"
        @sliding-end="onSlideEnd"
      >
        <b-carousel-slide
          v-for="(screenshot, index) in game.screenshots" :key="index"
          :img-src="screenshot.url.replace('t_thumb', 't_screenshot_med')"></b-carousel-slide>
      </b-carousel>
    </b-container>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    asyncData({params}){
      const cors = 'https://cors-anywhere.herokuapp.com/';
      return axios.get(`${cors}https://api-v3.igdb.com/games/${params.id}/?fields=name,cover.url,summary,platforms.name,screenshots.url,total_rating&expand=platforms,screenshots,cover`)
        .then(res => {
          return {
            game:res.data[0]
          }
        })
    }
  }
</script>
