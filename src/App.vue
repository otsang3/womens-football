<template lang="html">
  <div>
    <h1>FIFA 2019 Women's World Cup Football</h1>
    <filter-form :teamResults="groupResults" :countries="countries"
    :teams="teams"></filter-form>
    <team-detail v-if="selectedTeam" :selectedTeam="selectedTeam"></team-detail>
    <group-results-list :groupResults="groupResults"></group-results-list>
    <favourite-team-list :favourites="favourites"></favourite-team-list>
  </div>
</template>

<script>
import GroupResultsList from './components/GroupResultsList.vue';
import FilterForm from './components/FilterForm.vue';
import TeamDetail from './components/TeamDetail.vue';
import FavouriteTeamList from './components/FavouriteTeamList.vue';
import {eventBus} from './main.js';


export default {
  name: 'app',
  data(){
    return {
      groupResults: [],
      teams: [],
      selectedTeam: null,
      countries: []
    }
  },
  components: {
    'group-results-list': GroupResultsList,
    'filter-form': FilterForm,
    'team-detail': TeamDetail,
    'favourite-team-list': FavouriteTeamList
  },
  computed: {
    favourites: function(){
      return this.teams.filter(team => team.isFavourite === true);
    }
  },
  methods: {
    markFavourite: function(team){
      const index = this.teams.indexOf(team);
      this.teams[index].isFavourite = true;
    },
    unmarkFavourite: function(team){
      const index = this.teams.indexOf(team)
      this.teams[index].isFavourite = false;
    },
    sortTeams: function(property) {
    this.teams.sort((a, b) => {
    return a[property] < b[property] ? -1 : 1;
  })
  }
},
  mounted(){
    fetch('https://worldcup.sfg.io/teams/group_results')
    .then(response => response.json())
    .then(data => this.groupResults = data)

    fetch('https://worldcup.sfg.io/teams/')
    .then(response => response.json())
    .then(data => {
    const teamData = data.reduce(
    (flat, toFlatten) => flat.concat(toFlatten),
    []
    );
    teamData.forEach(team => (team.isFavourite = false));
    this.teams = teamData
    })
    .then(() => this.sortTeams("country"))


    // .then(data => this.teams = data.sort(function(a,b) {
    //   let nameA = a.country.toUpperCase();
    //   let nameB = b.country.toUpperCase();
    //   if (nameA < nameB) {
    //     return -1;
    //   }
    //   if (nameA > nameB) {
    //     return 1;
    //   }
    //   return 0;
    // }));

    fetch('https://restcountries.eu/rest/v2/all')
    .then(response => response.json())
    .then(data => this.countries = data);

    eventBus.$on('selectedTeam', (team) =>
    this.selectedTeam = team);

    eventBus.$on('favourite-added', selectedTeam => this.markFavourite(selectedTeam))

    eventBus.$on('favourite-removed', selectedTeam => this.unmarkFavourite(selectedTeam))
  }
}
</script>

<style lang="css" scoped>
</style>
