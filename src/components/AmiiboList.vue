<template lang="html">
  <div>
  <ul>
    <single-amiibo v-for="(amiibo, index) in amiibos.amiibo" :amiibo='amiibo' :key='index'></single-amiibo>
  </ul>



  </div>
</template>

<script>
import{eventBus} from '../main.js';
import listItem from './listItem.vue';
export default {
  name: 'amiibo-list',
  props: ['amiibos'],
  components:{
    'single-amiibo':listItem
  }
}
</script>

<style lang="css" scoped>
</style>
