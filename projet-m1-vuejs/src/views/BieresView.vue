<template>
  <div class="about">

    <div class="filtres">

      <div class="search-area">
        <form @submit.prevent="getBieresABV">
          <h3>Trouver une bière avec un taux alcool supérieur à</h3>
          <input style="border: none;border-bottom: 1px solid;margin-right: 5px;width: 30%;" type="number" v-model="taux_abv">
          <input style="border:none;background:#ffd400;text-transform:lowercase;padding:10px;border-radius:5px;" type="submit" name="Recherche bières" value="Rechercher">
        </form>
      </div>

      <div class="slider">
        <h3>Trouver une bière avec un IBU compris entre ... et ....</h3>
        <div class='range-slider'>
          <div class="range-number">
            <input type="range" style="margin-right:15px;" min=1 max=140 step="1" v-model="minIBU">
            <input type="number" min=1 max=140 step="1" v-model="minIBU">
          </div>
          <div class="range-number">
            <input type="range" style="margin-right:15px;" min=1 max=140 step="1" v-model="maxIBU">
            <input type="number" min=1 max=140 step="1" v-model="maxIBU">
          </div>
        </div>
      </div>

    </div>

    <div class="section-abv_gt">

      <div :key="index" v-for="(biere, index) in bieres" class="abv_gt">
        <div class="card-abv_gt">
          <h4>{{biere.name}}</h4>
          <p>Retrouvez les caractéristiques de chaques bières</p>
          <img :src="biere.image_url" alt="Image de la bière" width="80">
          <div class="caracteristique_abv">
            <ul>
              <li>Taux d'alcool: {{biere.abv}} %</li>
              <li>Niveau d'atténuation: {{biere.attenuation_level}}</li>
              <li>EBC: {{biere.ebc}}</li>
              <li>IBU: {{biere.ibu}}</li>
              <li>PH: {{biere.ph}}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<style>

  .section-abv_gt{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    margin-top: 100px;
  }

  .abv_gt{
    display: flex;
    align-items: center;
    width: 23%;
    margin-top: 50px;
    padding: 50px;
    border-radius: 50px;
  }

  .abv_gt:nth-child(odd){
    background: #e8c102;
  }

  .abv_gt:nth-child(even){
    background: #e87702;
  }

  .caracteristique_abv ul{
    padding: 0;
    margin-top: 50px;
    list-style: none;
  }

  .card-abv_gt h4{
    text-decoration: underline;
    margin-bottom: 30px;
  }

  .card-abv_gt p{
    margin-bottom: 30px;
  }

  .filtres{
    display: flex;
    justify-content: space-evenly;
    margin-top: 50px;
    margin-bottom: 30px;
  }

  #app .range-number input[type="number"] {
    background: #e8c102;
    border: none;
    padding: 5px;
    color: white;
    margin: 5px;
  }

</style>

<script>
import axios from 'axios'
import Vue from 'vue'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

export default {
  name: 'HomeView',
  data(){
    return{
      data: [],
      bieres: [],
      taux_abv: 0,
      count: 325,
      pageSize: 6,
      pageT: 1,
      minIBU: 1,
      maxIBU: 140,
    }
  },
  mounted(){
    axios
    .get(`https://api.punkapi.com/v2/beers`)
    .then((reponse) => {
      this.bieres = reponse.data;
      console.log(this.bieres)
    });
  },
  watch: {
    pageT() {
      axios.get('https://api.punkapi.com/v2/beers?per_page=' + this.pageSize + '&page=' + this.pageT)
      .then((resp)=>{
        this.bieres = resp.data;
      })
    },
    searchQuery() {
      this.minIBU = 1;
      this.maxIBU = 140;
      let match = '';
      if (this.searchQuery != '') {
        match = `&beer_name=${this.searchQuery}`
      }
      Vue.axios.get('https://api.punkapi.com/v2/beers?per_page=' + this.perPage + match)
      .then((resp)=>{
        this.bieres = resp.data;
        this.pageT = 1;
        this.count = this.bieres.length;
        if (this.searchQuery == '') {
          this.count = 325;
        }
      })
    },
    minIBU() {
      this.updateBiere();
    },
    maxIBU() {
      this.updateBiere();
    }
  },
  methods: {
    async getBieresABV(){
      await axios.get(`https://api.punkapi.com/v2/beers?abv_gt=${this.taux_abv}`)
      .then((reponse) =>{
        this.bieres = reponse.data
        console.log(this.data)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    slider: function() {
      if (this.minIBU > this.minIBU) {
        var tmp = this.maxPH;
        this.maxPH = this.minIBU;
        this.minIBU = tmp;
      }
    },
    updateBiere() {
      Vue.axios.get('https://api.punkapi.com/v2/beers?per_page=' + this.pageSize + '&ibu_gt=' + this.minIBU + '&ibu_lt=' + this.maxIBU)
      .then((resp)=>{
        this.bieres = resp.data;
        this.pageT = 1;
        this.count = this.bieres.length;
      })
    }
  },
}
</script>
