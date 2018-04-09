<template>
  <span>
    <img @click="toggleImage(true)" class="base base-mobile base-tablet base-desktop" :src="imagePath(url)" :style="{left: elPosX}">
    <transition name="fade" >
      <img  @click="toggleImage(false)" v-if="openedImage" class="big" :src="imagePath(url)">
    </transition>
  </span>
</template>

<script>
  export default {
    props: ['url', 'elPosX'],
    data() {
      return {
        openedImage: false
      }
    },
    methods: {
      imagePath(url) {
        return require('../assets/' + url + '.jpg')
      },
      toggleImage(value) {
        this.openedImage = value
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .base {
    position: relative;
    opacity: 1;
    margin: 10px;
    border: 5px solid white;
    border-radius: 10px;
    transition: opacity 1s, transform 1s;
    cursor: pointer
  }
  
  @media only screen and (max-width: 400px) {
    .base-mobile {
      max-width: 300px;
      max-height: 300px;
    }
  }
  
  @media only screen and (min-width: 400px) and (max-width: 1200px) {
    .base-tablet {
      max-width: 600px;
      max-height: 600px;
    }
  }
  
  @media only screen and (min-width: 1200px) {
    .base-desktop {
      width: auto;
      height: 400px;
    }
  }
  
  .base:hover {
    opacity: 0.2;
    transform: scale(1.1)

  }
  
  .big {
    border: 5px solid white;
    border-radius: 10px;
    position: absolute;
    max-height: 90%;
    max-width: 90%;
    margin: auto;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 100;
    cursor: pointer;
  }
</style>
