<template lang="html">
  <div>
    <h3 v-if="teamDetails">Team: {{teamDetails.country}}</h3>
    <img class="flagIcon" v-if="countryDetails"
    :src="countryDetails.flag" alt="no flag in API">
    <br>
    <p v-if="teamDetails">Wins: {{teamDetails.wins}}</p>
    <p v-if="teamDetails">Draws: {{teamDetails.draws}}</p>
    <p v-if="teamDetails">Losses: {{teamDetails.losses}}</p>
    <p v-if="teamDetails">Games Played: {{teamDetails.games_played}}</p>
    <p v-if="teamDetails">Points: {{teamDetails.points}}</p>
    <p v-if="teamDetails">Goals For: {{teamDetails.goals_for}}</p>
    <p v-if="teamDetails">Goals Against: {{teamDetails.goals_against}}</p>
    <p v-if="teamDetails">Goal Difference: {{teamDetails.goal_differential}}</p>
  </div>
</template>

<script>

export default {
  name: 'team-detail',
  data(){
    return {
    }
  },
  props: ['selectedTeam', 'teamDetails', 'countryDetails'],
}
</script>

}
<style lang="css" scoped>
h3 {
  float: left;
  padding-right: 0px;
}
.flagIcon {
  height: 25px;
  width: 50px;
  padding-top: 15px;
  padding-left: 10px;
  padding-bottom: 5px;
}
</style>
