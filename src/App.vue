<template lang="html">
  <div>
    <h1>Amiibo catalog</h1>
    <p>Amiibos you own</p>
<ul>
  <li v-for="(amiibo, index) in this.ownedAmiibo" :key='index'>{{amiibo.name}}</li>
</ul>
<select v-on:change="filter" v-model='selectedType'>
  <option value="">All</option>
  <option v-for="(type, index) in allTypes" :value="type">{{type}}</option>
</select>

    <amiibo-list :amiibos='filteredAmiibo' :ownedAmiibo='ownedAmiibo'></amiibo-list>
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
      ownedAmiibo: [],
      filteredAmiibo: [],
      selectedType: ""


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

    }
  },
  computed:{
    allTypes(){
      const types = this.amiibos.map(amiibo => amiibo.type)
      const uniType = Array.from(new Set(types))
      return uniType
    }
  }
}





</script>

<style lang="css" scoped>
</style>
