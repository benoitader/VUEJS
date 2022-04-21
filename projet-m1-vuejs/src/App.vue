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
          <router-link to="/bieres">Bieres</router-link>
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
  color: black;
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
}

.dot{
  width: 15px;
  height: 15px;
  background: #f5cc00;
  border-radius: 30px;
  margin-right: 15px;
  margin-left: 15px;
}

</style>
