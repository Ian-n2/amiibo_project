<template lang="html">
  <div>
    <h1>Amiibo catalog</h1>
    <p>Amiibos you own</p>
<ul>
  <li v-for="(amiibo, index) in this.ownedAmiibo" :key='index'>{{amiibo.name}}</li>
</ul>
    <amiibo-list :amiibos='amiibos' :ownedAmiibo='ownedAmiibo'></amiibo-list>
  </div>

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
      ownedAmiibo: []

    };
  },
  mounted(){
    fetch('https://www.amiiboapi.com/api/amiibo/')
    .then(res => res.json())
    .then(data => this.amiibos = data)

    eventBus.$on('addToOwned', (amiibo) =>{
      this.ownedAmiibo.push(amiibo);
    });
  },
  components: {
    "amiibo-list": AmiiboList
    // "single-amiibo": SingleAmiibo
  }
}





</script>

<style lang="css" scoped>
</style>
