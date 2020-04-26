<template lang="html">
  <div>
    <label>{{team.country}}</label>
    <button v-on:click="handleSubmit">View Stats</button>
    <button v-on:click="removeFavourite">Remove From Favourites</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: 'favourite-team-list-item',
  data() {
    return {
      selectedTeam: null
    }
  },
  props: ['team'],
  methods: {
    handleSubmit(){
      this.selectedTeam = this.team
      eventBus.$emit('view-details', this.selectedTeam)
    },
    removeFavourite(){
      eventBus.$emit('favourite-removed', this.team)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
