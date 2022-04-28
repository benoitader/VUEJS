<template>
  <div id="app">
    <div id="header">
      <div id="title-discobeer">
        <h1>Disco Beer</h1>
      </div>
      <div id="nav">
        <nav>
          <router-link to="/">Accueil</router-link>
          <div class="separation">-</div>
          <router-link to="/bieres">Filtra Bières</router-link>
        </nav>
      </div>
      <div id="logo">
        <img src="./assets/capsule.png" width="200px" alt="Image capsule bière">
      </div>
    </div>
    <router-view/>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

#app {
  font-family: 'Poppins', sans-serif;
  text-align: center;
}

body{
  margin: 0;
  background: url('./assets/tavern.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  color: white!important;
}

#home{
  max-width: 80%;
  margin: auto;
}

#header{
  height: 150px;
  display: flex;
  align-items: center;
  place-content: center;
}

#nav nav a{
  color: white;
  font-size: 25px;
  font-weight: bold;
  text-decoration: none;
  margin-right: 15px;
  margin-left: 15px;
}

#nav nav{
  display: flex;
  align-items: center;
  place-content: center;
}

#title-discobeer h1{
  text-decoration: underline;
}

#title-discobeer, #nav, #logo{
  width: 33%;
}

#home h2{
  text-align: left;
  font-size: 30px;
  margin: 0;
  margin-bottom: 45px;
}

#filtre-bieres{
  margin-bottom: 15px;
}

.dot-separation{
  display: flex;
  place-content: center;
  margin-top: 20px;
  margin-bottom: 20px;
}

.vitrine-biere:nth-child(even) .dot{
  width: 5px;
  height: 5px;
  background: #e8c102;
  border-radius: 30px;
  margin-right: 15px;
  margin-left: 15px;
}

.vitrine-biere:nth-child(odd) .dot{
  width: 5px;
  height: 5px;
  background: #e87702;
  border-radius: 30px;
  margin-right: 15px;
  margin-left: 15px;
}


#vitrine-discobeer{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 50px;
}

#vitrine-discobeer p{
  font-size: 13px;
}

.vitrine-biere{
  width: 30%;
  margin-bottom: 150px;
}

.cadre-img-biere{
  position: relative;
  display: flex;
  place-content: center;
  align-items: center;
  padding: 20px;
  border-radius: 20px;
  max-width: 275px;
  margin: auto;
  min-height: 400px;
}

.content-cadre{
  margin-bottom: 50px;
  width: 100%;
}

.cadre-img-biere::after{
  content: '';
  position: absolute;
  width: 100px;
  height: 100px;
  background-image: url(./assets/capsule.png);
  background-size: contain;
  bottom: -10%;
}

.vitrine-biere:nth-child(odd){
  background: #e8c10257;
  border-radius: 5px;
  padding: 10px;
}

.vitrine-biere:nth-child(even){
  background: #e8770257;
  border-radius: 5px;
  padding: 10px;
}

.vitrine-biere:nth-child(odd) .cadre-img-biere{
  background: #e8c102;
  margin-bottom: 50px;
}

.vitrine-biere:nth-child(even) .cadre-img-biere{
  background: #e87702;
  margin-bottom: 50px;
}

.cadre-img-biere .sup-img{
  text-align: right;
  font-size: 17px;
  color: white;
  font-weight: bold;
}

.cadre-img-biere .sup-img p{
  margin: 0;
}

.cadre-img-biere .sup-img p:nth-child(2){
  font-size: 13px;
  margin-top: 5px;
  text-transform: uppercase;
  color: #b79600;
}

.vitrine-biere:nth-child(even) .cadre-img-biere .sup-img p:nth-child(2){
  color: #e8c102;
}

.cadre-img-biere h3{
  color: white;
  font-size: 20px;
  text-decoration: underline;
}

.cadre-img-biere img{
  height: 150px;
}

.description-biere{
  text-align: left;
  max-width: 90%;
  margin: auto;
}

.pagination{
  margin-bottom: 50px;
  place-content: center;
}

#home .page-item.active .page-link{
  background-color: #e8c102;
  border-color: #e8c102;
  color: #fff;
}

#home .page-link{
  color: #e8c102;
}

#home .page-link:focus{
  box-shadow: 0 0 0 0.25rem rgb(232 193 2 / 26%);
}

.search-area input::placeholder{
  color: white;
}

</style>
