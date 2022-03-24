<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>POKEDEX</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div class="box">
        <input type="text" placeholder="Name....." v-model="search">
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
      console.log(this.pokemonList)
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
}

input[type="text"] {
  background: rgb(245, 245, 245);
  width: 390px;
  height: 40px;
  border: none;
  outline: none;
  padding: 0 25px;
  border-radius: 25px;
  margin-inline: 1%;

  font-size: 1rem;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
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