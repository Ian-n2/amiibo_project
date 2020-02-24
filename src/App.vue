<template lang="html">
  <div>
    <h1>Amiibo catalog</h1>
    <h2>Amiibos you own</h2>
    <!-- The code below is showing a orginsed list "with numbers" this loops from the amiibos
  added to the owned array and prints the name of each amiibo. -->
<ol>
  <li v-for="(amiibo, index) in this.ownedAmiibo" :key='index'>{{amiibo.name}}</li>
</ol>
<h3>Find the Amiibos you are looking for by type.</h3>
<!-- The code below is filtering all the amiibos by type. -->
<select v-on:change="filter" v-model='selectedType'>
  <option value="">All</option>
  <option v-for="(type, index) in allTypes" :value="type">{{type}}</option>
</select>
<h3>Find Amiibos that are in the games you love!!</h3>
<!-- The code below is filtering all the amiibos by the game. -->
<select v-on:change="filterGame" v-model='selectedGame'>
  <option value="">All</option>
  <option v-for="(game, index) in allGames" :value="game">{{gameSeries}}</option>
</select>
<amiibo-list :amiibos='filteredAmiibo' :ownedAmiibo='ownedAmiibo'></amiibo-list>

</div>
</template>

<script>
import {eventBus} from './main.js';
// this is passing down the amiibos and ownedAmiibo props to the AmiiboList component.
import AmiiboList from './components/AmiiboList.vue';

export default {
  name: 'app',
  data(){
    return{
      amiibos: [],
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

  },
  methods: {
    // This is the filter function.
    //It starts with us setting the filteredAmiibo to equal all the amiibos.
    //This is because the function is always showing the filtered list and at no point have it show
    // the all amiibo list.
    filter(){
      if (this.selectedType === "") {
        this.filteredAmiibo = this.amiibos

      } else {
// After the user picks a way they would like to filter the list this part of the function will run removing all the
//amiibos that dont match the selected type or game.
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
  // both of functions below are getting the amiibo by type/game.
  // then it is mapping all of those into an array.
  // after it has done that it is creating a new array and it is only putting in
  // unique values from the array it fisrt made. This is stopping me from getting 550
  // types returned as card and just getting one.

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
