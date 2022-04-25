<template>
  <div id="home">

    <h2>Recherchez la bières de votre choix</h2>

    <div class="search-area">
      <form @submit.prevent="getData">
        <input style="border: none;border-bottom: 1px solid;margin-right: 5px;width: 30%;" type="search" placeholder="Rechercher une bière" v-model="bieres">
        <input style="border:none;background:#ffd400;text-transform:lowercase;padding:10px;border-radius:5px;" type="submit" name="Recherche bières" value="Rechercher">
      </form>
    </div>

    <div id="vitrine-discobeer">

      <div :key="index" v-for="(bieres, index) in data.slice(0, 6)" class="vitrine-biere">

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
      data: [],
    }
  },
  methods: {
    async getData(){
      await axios.get(`https://api.punkapi.com/v2/beers?beer_name=${this.bieres}`)
      .then((reponse) =>{
        this.data = reponse.data
        console.log(this.data)
      })
      .catch((error) => {
        console.log(error)
      })
    }
  },
}
</script>
