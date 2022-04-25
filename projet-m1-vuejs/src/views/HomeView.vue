<template>
  <div id="home">

    <h2>Nos bières</h2>

    <div class="search-area">
      <input type="text" v-model="recherche" placeholder="Rechercher une bière" />
    </div>

    <div id="vitrine-discobeer">

      <div :key="index" v-for="(bieres, index) in bieres.slice(0, 6)" class="vitrine-biere">

        <div class="cadre-img-biere">
          <div class="content-cadre">
            <div class="sup-img">
              <p>{{bieres.tagline}}</p>
              <p>{{bieres.first_brewed}}</p>
            </div>
            <h3>{{bieres.name}}</h3>
            <img :src="bieres.image_url" alt="Image de la bière">
          </div>
        </div>

        <div class="description-biere">
          <div class="desc-biere">
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
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HomeView',
  data(){
    return{
      bieres: [],
      recherche: '',
    }
  },
  mounted(){
    axios
    .get('https://api.punkapi.com/v2/beers')
    .then((reponse) => {
      this.bieres = reponse.data;
    }).catch(erreur => this.bieres = [{title: "Erreur de chargement"}]);
  },
  computed: {
    filtreBieres: function(){
      return this.bieres.filter((biere) => {
        return biere.name.match(this.recherche);
      });
    }
  }
}
</script>
