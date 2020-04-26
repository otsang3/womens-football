<template lang="html">
  <div>
    <group-results-list-item v-for="(groupResult, index) in groupResults"
    :groupResult="groupResult" :key="index"></group-results-list-item>
  </div>
</template>

<script>
import GroupResultsListItem from './GroupResultsListItem.vue'

export default {
  name: 'group-results-list',
  props: ['groupResults'],
  components: {
    'group-results-list-item': GroupResultsListItem
  }
}
</script>

<style lang="css" scoped>
</style>
