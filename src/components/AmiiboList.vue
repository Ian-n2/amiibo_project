<template lang="html">
  <div>
    <!-- <select id="amiibo_select">
      <option v-for="(amiibo, index) in amiibos"
      :value="amiibo" :key="index">{{amiibo.type}}</option>

    </select> -->
  <ul>
    <single-amiibo v-for="( amiibo,index) in amiibos.amiibo" :amiibo='amiibo' :key='index'></single-amiibo>
  </ul>


  </div>
</template>

<script>
import{eventBus} from '../main.js';
import listItem from './listItem.vue';
export default {
  name: 'amiibo-list',
  data(){
    return{
      selectedAmiibo:[]
    }
  },
  props: ['amiibos'],
  components:{
    'single-amiibo':listItem
  },
  // handleClick(){
  //   eventBus.;$emit("amiibo-selected", this.selectedAmiibo)
  // }
}
</script>

<style lang="css" scoped>
</style>
