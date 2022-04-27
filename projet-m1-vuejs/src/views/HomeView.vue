<template>
  <div id="home">

    <h2>Recherchez la bières de votre choix</h2>

    <div class="search-area">
      <form @submit.prevent="getData">
        <input style="border: none;border-bottom: 1px solid;margin-right: 5px;width: 30%;" type="search" placeholder="Rechercher une bière" v-model="query">
        <input style="border:none;background:#ffd400;text-transform:lowercase;padding:10px;border-radius:5px;" type="submit" name="Recherche bières" value="Rechercher">
      </form>
    </div>

    <div id="vitrine-discobeer">

      <div :key="index" v-for="(biere, index) in bieres" class="vitrine-biere">

        <div class="cadre-img-biere">
          <div class="content-cadre">
            <div class="sup-img">
              <p>{{biere.tagline}}</p>
              <p>{{biere.first_brewed}}</p>
            </div>
            <h3>{{biere.name}}</h3>
            <img :src="biere.image_url" alt="Image de la bière">
          </div>
        </div>

        <div class="description-biere">
          <div class="desc-biere">
            <h3>{{biere.name}}</h3>
            <p>{{biere.description}}</p>
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
            <p>{{biere.brewers_tips}}</p>
          </div>
        </div>

      </div>

    </div>

    <b-pagination
      v-model="pageT"
      :total-rows="count"
      :per-page="pageSize"
      pills
    ></b-pagination>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HomeView',
  data(){
    return{
      data: [],
      bieres: [],
      count: 325,
      pageSize: 6,
      pageT: 1,
      query: "",
    }
  },
  watch: {
    pageT() {
      axios.get('https://api.punkapi.com/v2/beers?per_page=' + this.pageSize + '&page=' + this.pageT)
      .then((resp)=>{
        this.bieres = resp.data;
      })
    },
  },
  methods: {
    async getData(){
      await axios.get(`https://api.punkapi.com/v2/beers?beer_name=${this.query}`)
      .then((reponse) =>{
        this.bieres = reponse.data
        console.log(this.data)
      })
      .catch((error) => {
        console.log(error)
      })
    }
  },
  mounted(){
    axios
    .get(`https://api.punkapi.com/v2/beers?per_page=${this.pageSize}`)
    .then((reponse) => {
      this.bieres = reponse.data;
      console.log(this.bieres)
    });
  },
}
</script>
