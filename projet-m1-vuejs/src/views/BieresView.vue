<template>
  <div class="about">

    <div class="search-area">
      <form @submit.prevent="getBieresABV">
        <h3>Trouver une bière avec un taux alcool supérieur à</h3>
        <input style="border: none;border-bottom: 1px solid;margin-right: 5px;width: 30%;" type="number" v-model="taux_abv">
        <input style="border:none;background:#ffd400;text-transform:lowercase;padding:10px;border-radius:5px;" type="submit" name="Recherche bières" value="Rechercher">
      </form>
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
              <li>PH: {{biere.ph}}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <MultiRangeSlider
      :baseClassName="multi-range-slider"
      :min="0"
      :max="100"
      :step="10"
      :ruler="true"
      :label="true"
      :minValue="barMinValue"
      :maxValue="barMaxValue"
      @input="UpdateValues"
    />

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

</style>

<script>
import axios from 'axios'
import MultiRangeSlider from "multi-range-slider-vue";

export default {

  components: {
      MultiRangeSlider
  },

  data(){
    return{
      data: [],
      bieres: [],
      taux_abv: 0,
      barMinValue: 10,
      barMaxValue: 90
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

    UpdateValues(e) {
      this.barMinValue = e.minValue;
      this.barMaxValue = e.maxValue;
    }
    
  },
}
</script>
