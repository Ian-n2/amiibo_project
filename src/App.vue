<template lang="html">
  <div>
    <h1>Amiibo catalog</h1>
    <h2>Amiibos you own</h2>
<ol>
  <li v-for="(amiibo, index) in this.ownedAmiibo" :key='index'>{{amiibo.name}}</li>
</ol>
<h3>Find the Amiibos you are looking for by type.</h3>
<select v-on:change="filter" v-model='selectedType'>
  <option value="">All</option>
  <option v-for="(type, index) in allTypes" :value="type">{{type}}</option>
</select>
<h3>Find Amiibos that are in the games you love!!</h3>
<select v-on:change="filterGame" v-model='selectedGame'>
  <option value="">All</option>
  <option v-for="(game, index) in allGames" :value="game">{{gameSeries}}</option>
</select>
<amiibo-list :amiibos='filteredAmiibo' :ownedAmiibo='ownedAmiibo'></amiibo-list>

</div>
</template>

<script>
import {eventBus} from './main.js';
import AmiiboList from './components/AmiiboList.vue';
// import SingleAmiibo from './components/listItem.vue';

export default {
  name: 'app',
  data(){
    return{
      amiibos: [],
      selectedAmiibo:null,
      ownedAmiibo: [],
      filteredAmiibo: [],
      selectedType: "",
      selectedGame: ""


    };
  },
  mounted(){
    fetch('https://www.amiiboapi.com/api/amiibo/')
    .then(res => res.json())
    .then(data => {
      this.amiibos = data.amiibo
      this.filteredAmiibo = this.amiibos
    })

    eventBus.$on('addToOwned', (amiibo) =>{
      this.ownedAmiibo.push(amiibo);
    });
  },
  components: {
    "amiibo-list": AmiiboList
    // "single-amiibo": SingleAmiibo
  },
  methods: {
    filter(){
      if (this.selectedType === "") {
        this.filteredAmiibo = this.amiibos

      } else {

        const filtered = this.amiibos.filter(amiibo => {
          return amiibo.type === this.selectedType

        });
        this.filteredAmiibo = filtered

    }
  },
    filterGame(){
      if (this.selectedGame === "") {
        this.filteredAmiibo = this.amiibos

      } else {

        const byGame = this.amiibos.filter(amiibo => {
          return amiibo.gameSeries === this.selectedGame

        });
        this.filteredAmiibo = byGame
      }
    }

  },
  computed:{
    allTypes(){
      const types = this.amiibos.map(amiibo => amiibo.type)
      const uniType = Array.from(new Set(types))
      return uniType
    },
    allGames(){
      const games = this.amiibos.map(amiibo => amiibo.gameSeries)
      const uniGame = Array.from(new Set(games))
      return uniGame
    }

    }
  }






</script>

<style lang="css" scoped>
div{
background-image: url('../public/nintendo1.png');
text-align: center;
font-family: monospace;
}
</style>
