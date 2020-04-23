<template lang="html">
  <p v-on:click="handleClick">{{beer.name}}</p>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'beer-item',
  props: ['beer'],
  methods: {
    handleClick() {
      eventBus.$emit('beer-selected', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
