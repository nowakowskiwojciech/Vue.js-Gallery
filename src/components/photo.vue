<template>
  <span>
        <img @click="open" class="base" :src="imagePath(url)" :style="{left: styl}">
        <transition  name="fade" >
          <img  @click="close" v-if="opened" class="big" :src="imagePath(url)">
        </transition>
      </span>
</template>

<script>
  export default {
    props: ['url', 'styl'],
    data() {
      return {
        opened: false
      }
    },
    methods: {
      imagePath(url) {
        return require('../assets/' + url + '.jpg')
      },
      open() {
        this.opened = true
      },
      close() {
        this.opened = false
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .base {
    position: relative;
    opacity: 1;
    width: auto;
    height: 400px;
    margin: 10px;
    border: 5px solid white;
    border-radius: 10px;
    transition: opacity 1s;
    cursor: pointer
  }
  
  .base:hover {
    opacity: 0.2;
  }
  
  .big {
    border: 5px solid white;
    border-radius: 10px;
    position: absolute;
    max-height: 90%;
    width: auto;
    margin: auto;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 1000;
  }
</style>
