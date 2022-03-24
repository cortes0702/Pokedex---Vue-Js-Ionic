<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title></ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content >
      <ion-input placeholder="Enter Input"></ion-input>
      <div class="contenido">
            <ion-card v-for="type in pokeTypes" :key="type" class="cards">
            <ion-button class="btnType" @click="searchType(type)">
                <ion-card-content>
                    <ion-label>{{ type.name }}</ion-label>
                </ion-card-content>
            </ion-button>
        </ion-card>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import axios from 'axios';

export default defineComponent({
  name: 'Tab3Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  data(){
    return {
      pokeTypes:[{img:'../../resources/img/types/Normal.png', name:'Normal'},{img:'../../resources/img/types/Fighting.png', name:'Fighting'},
                 {img:'../../resources/img/types/Poison.png', name:'Poison'},{img:'../../resources/img/types/Flying.png', name:'Flying'},
                 {img:'../../resources/img/types/Ground.png', name:'Ground'},{img:'../../resources/img/types/Rock.png', name:'Rock'},
                 {img:'../../resources/img/types/Bug.png', name:'Bug'},{img:'../../resources/img/types/Ghost.png', name:'Ghost'},
                 {img:'../../resources/img/types/Steel.png', name:'Steel'},{img:'../../resources/img/types/Fire.png', name:'Fire'},
                 {img:'../../resources/img/types/Water.png', name:'Water'},{img:'../../resources/img/types/Grass.png', name:'Grass'},
                 {img:'../../resources/img/types/Electric.png', name:'Electric'},{img:'../../resources/img/types/Physics.png', name:'Physics'},
                 {img:'../../resources/img/types/Ice.png', name:'Ice'},{img:'../../resources/img/types/Dragon.png', name:'Dragon'}, 
                 {img:'../../resources/img/types/Dark.png', name:'Dark'},{img:'../../resources/img/types/Fairy.png', name:'Fairy'}],
      pokemonsTotal: '',
      search: []
    }
  },
  async mounted(){
    const res = await axios.get("https://pokeapi.co/api/v2/pokemon/")
    this.pokemonsTotal = res.data.count
  },
  methods:{
    async searchType(){
      const total = this.pokemonsTotal
      for (let i = 1; i <= parseInt(total); i++) {
        const res = await axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)
        this.search.push(res.data)
        console.log(this.search)
        
      }
    }
  }
});
</script>
