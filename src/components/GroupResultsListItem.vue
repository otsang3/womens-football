<template lang="html">
  <div class="border">
    <h2>Group {{groupResult.letter}}</h2>
    <p>{{groupResult.ordered_teams[0].country}}</p>
    <p>{{groupResult.ordered_teams[1].country}}</p>
    <p>{{groupResult.ordered_teams[2].country}}</p>
    <p>{{groupResult.ordered_teams[3].country}}</p>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'group-results-list-item',
  data(){
    return{
      abc: null
    }
  },
  props: ['groupResult'],
}
</script>

<style lang="css" scoped>
.border {
  box-sizing: border-box;
  width: 400px;
  height: 250px;
  padding-left: 25px;
  padding-top: 10px;
  border-style: solid;
}
</style>
