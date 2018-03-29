<template>
  <div id="app" class="container">
    <div class='srodek' :style="{top: top2, opacity: opa}">
      <h1 class='cat' @click="showx.abstract=true, top2 = '-20%', opa = '0'">Abstraction</h1>
      <h1 class='cat' @click="showx.music=true, top2 = '-20%', opa = '0' ">Music</h1>
      <h1 class='cat' @click="showx.animals=true, top2 = '-20%', opa = '0' ">Animals</h1>
      <h1 class='cat' @click="showx.nature=true, top2 = '-20%', opa = '0' ">Nature</h1>
    </div>
    <transition class='row' name="fade">
      <h1 v-if="showx.abstract || showx.music || showx.animals" @click="showx.abstract=false, showx.music=false, showx.animals=false, top2='50%', opa='1' " align="left">Back</h1>
    </transition>
  
    <transition name="fade">
      <category v-if="showx.abstract" :photos="category.abstract" />
    </transition>
    <transition name="fade">
      <category v-if="showx.music" :photos="category.music" />
    </transition>
    <transition name="fade">
      <category v-if="showx.animals" :photos="category.animals" />
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
        top2: "50%;",
        opa: "1",
        category: {
          music: ['m1', 'm2', 'm3', 'm4', 'm5'],
          abstract: ['a1', 'a2', 'a3', 'a4', 'a5', 'a6', 'a7', 'a8'],
          animals: [1, 2, 3, 4, 5, 6, 7, 8]
        },
        showx: {
          music: false,
          abstract: false,
          animals: false
        }
  
      }
    },
    methods: {},
    computed: {
      showCategory(value) {
  
        return value
  
      }
  
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
