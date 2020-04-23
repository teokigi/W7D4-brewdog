<template lang="html">
  <div id="container">
    <div class="left">
      <h1>Brewdog Beers</h1>
      <beer-list :beers="beers"></beer-list>
    </div>

    <div class="right">
      <div class="details">
        <h1>Beer Details</h1>
        <beer-detail v-if="selectedBeer" :beer="selectedBeer"></beer-detail>
      </div>
      <div class="favourites">

        <h1>Favourite Beers</h1>
        <div class="favourites">

        <p v-for="favouriteBeer of favouriteBeers">{{favouriteBeer.name}} <button v-on:click="removeFavourite(favouriteBeer)">Remove from favourites</button></p>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import BeerList from './components/BeerList.vue'
import {eventBus} from './main.js'
import BeerDetails from './components/BeerDetails.vue'

export default {
  name: 'app',
  data(){
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: []
    }
  },
  mounted() {
    this.getBeers()

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer;

    eventBus.$on('fave-beer', (beer) => {
      if(!this.favouriteBeers.includes(beer)) {
        this.favouriteBeers.push(beer)
      }
    })
    })
  },
  methods: {
    getBeers: function(){
      fetch("https://api.punkapi.com/v2/beers?page=1&per_page=80")
      .then(res => res.json())
      .then(beers => this.beers = beers)
      fetch("https://api.punkapi.com/v2/beers?page=2&per_page=80")
      .then(res => res.json())
      .then(beers => beers.forEach(beer => this.beers.push(beer)))
      fetch("https://api.punkapi.com/v2/beers?page=3&per_page=80")
      .then(res => res.json())
      .then(beers => beers.forEach(beer => this.beers.push(beer)))
      fetch("https://api.punkapi.com/v2/beers?page=4&per_page=80")
      .then(res => res.json())
      .then(beers => beers.forEach(beer => this.beers.push(beer)))
      fetch("https://api.punkapi.com/v2/beers?page=5&per_page=80")
      .then(res => res.json())
      .then(beers => beers.forEach(beer => this.beers.push(beer)))
    },
    removeFavourite: function(beer){
      this.favouriteBeers = this.favouriteBeers.filter(favBeer => !(favBeer === beer))}
  },
  components: {
    'beer-list': BeerList,
    'beer-detail': BeerDetails
  }
}
</script>

<style lang="css" scoped>
  #container {
    display: flex;
    justify-content: center;
    width: 100%;
    background-image: url("https://images.unsplash.com/photo-1571613316887-6f8d5cbf7ef7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1651&q=80");
    color: white;
    text-shadow: 0px 0px 4px black, 0px 0px 4px black, 0px 0px 8px black;
    font-size: 1.5em;
  }

  .left {
    width: 500px;
  }

  .right {
    width: 500px;
    /* background-color: black;
    background-blend-mode: color-dodge; */
  }

  .details{
    /* background-color: beige; */
  }

  .favourites{
    /* background-color: beige; */
  }

  div{
    /* border-style: solid; */
    /* border-radius: 10px; */
    padding: 10px;
  }
</style>
