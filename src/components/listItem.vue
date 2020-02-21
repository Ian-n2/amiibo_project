<template lang="html">
  <div id="amiiboDetail">
    <div>
       <h2>{{amiibo.name}}</h2>
       <p>{{amiibo.type}}</p>
       <img :src="amiibo.image">

      </div>



  </div>
</template>

<script>
import{eventBus} from '../main.js'
export default {
  name: 'single-amiibo',
  props:["amiibo"]

    }


</script>

<style lang="css" scoped>
img{
  height: 160px;
  width: 100px;
}

#amiiboDetail{
  margin: 30px;
  display: inline-block;
}
</style>
