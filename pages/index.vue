<template>
  <div>
    <h1>Inicio</h1>
  </div>
</template>

<script>
import axios from 'axios'

axios.defaults.headers.common['user-key'] = 'aaa';
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
        return {
          games:res.data
        }
      })
  }
}
</script>
