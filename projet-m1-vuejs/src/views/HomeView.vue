<template>
  <div class="home">

    <div :key="index" v-for="(bieres, index) in bieres" id="vitrine-biere">
      <h1>{{bieres.name}}</h1>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HomeView',
  data(){
    return{
      bieres: null,
    }
  },
  mounted(){
    axios
    .get('https://api.punkapi.com/v2/beers')
    .then((reponse) => {
      this.bieres = reponse.data;
      console.log(this.bieres)
    });
  },
}
</script>
