<template lang="html">
  <div id="amiiboDetail">
    <div>
       <h2>{{amiibo.name}}</h2>
       <p>{{amiibo.amiiboSeries}}</p>
       <img :src="amiibo.image">
<br>
<div v-if="!ownedAmiibo.includes(amiibo)" >

<button type="submit" v-on:click='handleClick'
:value='amiibo' name='ownedAmiibo'>own</button>
      </div>


    </div>


  </div>
</template>

<script>
import{eventBus} from '../main.js'
export default {
  name: 'single-amiibo',
  props:["amiibo", "ownedAmiibo"],
  methods:{
    handleClick(){
      eventBus.$emit('addToOwned', this.amiibo)
    }
  }

    }


</script>

<style lang="css" scoped>
img{
  height: 160px;
  width: 100px;
  border-color: red;

}

#amiiboDetail{
  margin: 30px;
  display: inline-block;
  text-align: center;
}
</style>
