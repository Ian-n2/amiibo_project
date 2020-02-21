<template lang="html">
  <div>
    <h1>Amiibo!!</h1>
  <amiibo-list :amiibos='amiibos'></amiibo-list>
</div>

  </div>
</template>

<script>
import {eventBus} from './main.js';
import AmiiboList from './components/AmiiboList.vue';

export default {
  name: 'app',
  data(){
    return{
      amiibos: [],
      selectedAmiibo:null,

    };
  },
  mounted(){
    fetch('https://www.amiiboapi.com/api/amiibo/')
    .then(res => res.json())
    .then(data => this.amiibos = data)
  },
  components: {
    "amiibo-list": AmiiboList
  }


  }

</script>

<style lang="css" scoped>
</style>
