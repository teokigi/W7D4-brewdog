<template lang="html">
  <div>
    <h3>{{beer.name}}</h3>
    <p>ABV: {{beer.abv}}</p>
    <p>Description:</p>
    <p> {{beer.description}}</p>
    <p>Hops:</p>
    <ul>
      <li v-for="ingredient of filterIngredients()">{{ingredient}}</li>
    </ul>
    <p>Malts:</p>
    <ul>
      <li v-for="ingredient of beer.ingredients.malt">{{ingredient.name}}</li>
    </ul>
    <p>Yeast: {{beer.ingredients.yeast}}</p>
    <button v-on:click="saveBeer" type="button" name="button">Add to favourites</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'beer-detail',
  props: ['beer'],
  methods: {
    saveBeer() {
      eventBus.$emit('fave-beer', this.beer)
    },
  filterIngredients(){
     return this.beer.ingredients.hops.map(ingredient => ingredient.name)
     .filter((name, index, array) =>array.indexOf(name) === index);
    }
  }


}
</script>

<style lang="css" scoped>
</style>
