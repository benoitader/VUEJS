<template>
  <div id="home">

    <h2>Nos bières</h2>

    <div id="filtre-bieres">
      Filtre ici
    </div>

    <div :key="index" v-for="(bieres, index) in bieres" class="vitrine-biere">

      <div class="cadre-img-biere">
        <div class="sup-img">
          <p>{{bieres.tagline}}</p>
          <p>{{bieres.contributed_by}}</p>
        </div>
        <h3>{{bieres.name}}</h3>
        <img :src="bieres.image_url" alt="Image de la bière">
      </div>

      <div class="description-biere">
        <h3>{{bieres.name}}</h3>
        <p>{{bieres.description}}</p>
      </div>

      <div class="dot-separation">
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
      </div>

      <div class="tips">
        <p>{{bieres.brewers_tips}}</p>
      </div>

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
