<template>
  <div id="app" class="container">
    <div  class='srodek' :style="{top: top2, opacity: opa}">
      <h1 v-for="album in albums" :key="album" class='cat' @click="currentAlbum = album, top2 = '-20%', opa = '0'">{{album}}</h1>
    </div>
  
    <div style="text-align:left; margin-top:50px;">
      <transition name="fade">
        <span class='cat' v-if="currentAlbum != null" style='cursor:pointer' @click="currentAlbum = null, top2='50%', opa='1'" align="left">Back</span>
      </transition>
    </div>

    <transition name="fade">
      <category v-if="album = currentAlbum" :v-for="album in albums" :photos="photoNames[currentAlbum]" />
    </transition>
  </div>
</template>

<script>
  import category from './components/category'
  export default {
    name: 'App',
    components: {
      category
    },
    data() {
  
      return {
        top2: "-20%",
        opa: "1",
        photoNames: {
          music: ['m1', 'm2', 'm3', 'm4', 'm5', 'm6', 'm7', 'm8'],
          abstract: ['a1', 'a2', 'a3', 'a4', 'a5', 'a6', 'a7', 'a8'],
          animals: ['an1', 'an2', 'an3', 'an4', 'an5', 'an6', 'an7', 'an8']
        },
        albums: ['abstract', 'music', 'animals', 'nature'],
        currentAlbum: null
  
      }
    },
    methods: {
    },
    created() {
      var that = this;
      setTimeout(function() {
        that.top2 = "50%"
      }, 500);
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: white;
    font-size: 50px;
  }
  
  body {
    background-color: black
  }
  
  .srodek {
    transition: top 2s, opacity 2s;
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-right: -50%;
    transform: translate(-50%, -50%)
  }
  
  .cat {
    position: relative;
    transition: font-size 2s;
    cursor: pointer;
  }
  
  .cat:hover {
    font-size: 80px;
  }
</style>
