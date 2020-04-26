<template lang="html">
  <div>
    <h2>Favourite Teams</h2>
    <favourite-team-list-item v-for="(team,index) in favourites"
    :team="team" :index="index"></favourite-team-list-item>
  </div>
</template>

<script>
import FavouriteTeamListItem from './FavouriteTeamListItem.vue'
export default {
  name: 'favourite-team-list',
  props: ['favourites'],
  components: {
    'favourite-team-list-item': FavouriteTeamListItem
  }
}
</script>

<style lang="css" scoped>
</style>
