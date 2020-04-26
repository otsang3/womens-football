<template lang="html">
  <div>
    <label>Select a Country: </label>
    <select v-on:change="handleSelect" v-model="selectedTeam" >
      <option disabled on value="">Countries</option>
      <option v-for="team in teams" :value="team">{{team.country}}</option>
    </select>
    <button v-on:click="addFavourite">Add To Favourite Teams</button>
    <team-detail :teamDetails="teamDetails" :countryDetails="countryDetails"></team-detail>
  </div>
</template>

<script>
import {eventBus} from '../main.js';
import TeamDetail from './TeamDetail.vue';

export default {
  name: 'filter-form',
  data(){
    return {
      selectedTeam: null,
      search: "",
      teamDetails: null,
      countryDetails: null
    }
  },
  props: ['teams', 'teamResults', 'countries'],
  components: {
    'team-detail': TeamDetail
  },
  methods: {

    handleSelect(){
      eventBus.$emit('selectedTeam', this.selectedTeam)

      // method used to retrieve team data from another API
      let foundArr = this.teamResults.find(teamResult =>
        teamResult.ordered_teams.find(team => team.country == this.selectedTeam.country))

      let foundTeam = (foundArr.ordered_teams.find(team => team.country == this.selectedTeam.country))

      this.teamDetails = foundTeam

      // method used to retrieve country flag images from another API
      let foundCountry = this.countries.find(country =>
      country.name == this.selectedTeam.country)

      this.countryDetails = foundCountry
    },
    addFavourite: function() {
      eventBus.$emit('favourite-added', this.selectedTeam);
      console.log(this.selectedTeam);
    }
  },
  mounted() {
    eventBus.$on('view-details', (selectedTeam) =>
    this.selectedTeam = selectedTeam)

  }
}
</script>
<style>
</style>
