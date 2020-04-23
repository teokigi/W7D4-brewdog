<template lang="html">
  <div>
    <h3>{{beer.name}}</h3>
    <p>ABV: {{beer.abv}}</p>
    <p>Description: {{beer.description}}</p>
    <p>Hops:</p>
    <ul>
      <li v-for="ingredient of beer.ingredients.hops">{{ingredient.name}}</li>
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
  data() {
    return {
    beerIngredients: null
    }
  },
  methods: {
    saveBeer() {
      eventBus.$emit('fave-beer', this.beer)
    }
  },
  computed: {
  removeDuplicate: function(){
      return this.beer.ingredients.hops.map((ingredient) => {
        return ingredient.name;
      })
      .filter((name, index, array) => {
        return array.indexOf(name) === index;
      });
    }
  }
}
</script>

<style lang="css" scoped>
</style>
