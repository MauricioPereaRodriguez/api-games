<template>
  <div>
    <b-container class="mt-3">
      <b-row>
        <b-col cols="4" v-for="game in games" :key="game.id">
          <b-card
            :title="game.name"
            :img-src="game.cover.url.replace('t_thumb', 't_cover_big')"
            img-alt="Imagen"
            img-top
            style="max-width: 20rem;">
            <p class="card-text">{{game.genres[0].names}}</p>
            <nuxt-link :to="'/games/' + game.id" class="btn btn-primary">Ver más... </nuxt-link>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from 'axios'

axios.defaults.headers.common['user-key'] = 'aaa'; // Cambiar por key-secret
axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';

export default {
  data(){
    return {
      games: [

      ]
    }
  },
  asyncData() {
    const cors = 'https://cors-anywhere.herokuapp.com/';
    return axios.get(`${cors}https://api-v3.igdb.com/games/?fields=name,genres.name,cover.url,popularity&order=popularity:desc&expand=genres`)
      .then(res => {
        //console.log(res);
        return {
          games:res.data
        }
      })
  }
}
</script>
