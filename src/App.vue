<template>
  <div id="app" class="container">
    <div class='albums-center' :style="{top: textTop, opacity: textOpacity}">
      <h1 v-for="album in albums" :key="album" class='text' @click="currentAlbum = album, backLeft='0%', backOpacity='1', textTop = '-20%', textOpacity = '0'">{{album}}</h1>
    </div>
  
    <div class='back'>
      <transition name="fade">
        <span :style="{left: backLeft, opacity: backOpacity }" class='text' @click="currentAlbum = null, backLeft='-20%', backOpacity='0',  textTop='50%', textOpacity='1'">back</span>
      </transition>
    </div>
  
    <transition name="slide-fade">
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
        backOpacity: "0",
        backLeft: "-20%",
        textTop: "-20%",
        textOpacity: "1",
        photoNames: {
          music: ['m1', 'm2', 'm3', 'm4', 'm5', 'm6', 'm7', 'm8'],
          abstract: ['a1', 'a2', 'a3', 'a4', 'a5', 'a6', 'a7', 'a8'],
          animals: ['an1', 'an2', 'an3', 'an4', 'an5', 'an6', 'an7', 'an8'],
          nature: ['n1', 'n2', 'n3', 'n4', 'n5', 'n6', 'n7', 'n8']
  
        },
        albums: ['abstract', 'music', 'animals', 'nature'],
        currentAlbum: null
  
      }
    },
    methods: {},
    created() {
      var that = this;
      setTimeout(function() {
        that.textTop = "50%"
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
    background-color: black;
    overflow: hidden
  }
  
  .albums-center {
    transition: top 2s, opacity 2s;
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-right: -50%;
    transform: translate(-50%, -50%)
  }
  
  .text {
    position: relative;
    transition: all 1s;
    cursor: pointer;
  }
  
  .text:hover {
    font-size: 80px;
  }
  
  .slide-fade-enter-active {
    transition: all 2s ease;
  }
  
  .slide-fade-leave-active {
    transition: all 2s ease;
  }
  
  .slide-fade-enter,
  .slide-fade-leave-to
  /* .slide-fade-leave-active below version 2.1.8 */
  
  {
    transform: translateX(500px);
    opacity: 0;
  }
  
  .back {
    text-align: left;
    margin-top: 50px;
  }
</style>
