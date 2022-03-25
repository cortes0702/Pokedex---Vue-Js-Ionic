<template>
  <ion-page>
    <ion-header translucent>
      <ion-toolbar>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div class="box">
        <input type="text" placeholder=" Search" v-model="search">
      </div>
      <div class="content">
        <ion-card v-for="pokemon in filteredPokemon" :key="pokemon.id" class="targets">
          <ion-card-content class="card">
            <img :src="pokemon.sprites.front_default" class="sprite">
            <ion-label class="name">{{ pokemon.name.toUpperCase() }}</ion-label>
          </ion-card-content>
        </ion-card>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';

//Importamos axios
import axios from 'axios';

export default defineComponent({
  name: 'Tab2Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  data(){
    return {
      search: "",
      pokemonList: []
    }
  },
  async mounted(){
    for (let i = 1; i < 898; i++) {
      const res = await axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)
      this.pokemonList.push(res.data)
      //console.log(this.pokemonList)
    }
  },
  computed: {
    filteredPokemon() {
      return this.pokemonList.filter(pokemonList => pokemonList.name.includes(this.search))
    }
  }
});
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Acme");

* {
  margin: 0;
  padding: 0;
  scroll-behavior: smooth;
}

.box {
  display: flex;
  justify-content: center;
  margin: auto;
  margin-top: 3%;
  margin-bottom: 1%;
  position: relative;
}

input {
  position: relative;
  display: inline-block;
  font-size: 20px;
  box-sizing: border-box;
  transition: .5s;
  text-align: center;
}

input[type="text"] {
  background: rgb(250, 250, 250);
  width: 335px;
  height: 40px;
  border: 1px solid rgb(184, 184, 184);
  outline: none;
  padding: 0 25px;
  border-radius: 25px;
  margin-inline: 1%;

  font-size: .8rem;
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
}

input:focus {
  width: 360px;
  transition: .3s;
}

.content {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.targets {
  width: 30%;
  height: 147px;
  background-color: rgb(252, 252, 252);
  margin: 1.5%;
}

.sprite {
  display: flex;
  justify-content: center;
  margin: auto;
  background-image: url("../../resources/blob.svg");
  margin-top: 8%;
}

.name {
  display: flex;
  justify-content: center;
  margin: auto;

  font-family: 'Acme', arial;
  font-size: 1rem;
  font-weight: normal;
  color: black;
}
</style>