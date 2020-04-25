<template lang="html">
  <div>
    <beer-item v-for="beer of beers" :beer="beer"></beer-item>
  </div>
</template>

<script>
import BeerItem from './BeerItem.vue'

export default {
  name: 'beer-list-derp',
  props: ['beers'],
  components: {
    'beer-item': BeerItem
  }
}
</script>

<style lang="css" scoped>
</style>
