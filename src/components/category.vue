<template>
  <div>
    <div class='display'>
      <photo v-for="photo in photos" :elPosX="elPos" :url="photo" :key="photo">
      </photo>
    </div>
    <div class='center-arrow'>
      <img src="../assets/arrow-l.png" class='arrow' @mouseover="startAnimation('left')" @mouseleave="stopAnimation('left')">
      <img src="../assets/arrow-r.png" class='arrow' @mouseover="startAnimation('right')" @mouseleave="stopAnimation('right')">
    </div>
  </div>
</template>

<script>
  import photo from '../components/photo'
  
  export default {
    props: ['photos'],
    name: 'Category',
    components: {
      photo
    },
    data() {
      return {
        elPos: 0,
        elX: 0,
        speed: 0,
        friction: 0.2,
        maxSpeed: 8,
        oneIntervalStart: true,
        oneIntervalStop: true
      }
    },
    methods: {
      startAnimation(value) {
        var that = this;
  
        if (this.oneIntervalStart == true) {
          window.var = setInterval(function() {
            that.elX += that.speed;
            that.elPos = that.elX + 'px'
          }, 20);
          window.el = setInterval(function() {
            if (value == 'right') {
              that.speed += that.friction;
              if (that.speed >= that.maxSpeed) {
                clearInterval(window.el);
              }
            } else {
              that.speed -= that.friction;
              if (that.speed <= -that.maxSpeed) {
                clearInterval(window.el);
              }
  
            }
          }, 30)
          this.oneIntervalStart = false;
        }
      },
      stopAnimation(value) {
        clearInterval(window.el);
  
        var that = this;
        if (this.oneIntervalStop == true) {
          window.slizg = setInterval(function() {
            if(value == 'right'){
              that.speed -= that.friction
              if (that.speed <= 0) {
                clearInterval(window.var);
                that.oneIntervalStart = true;
                clearInterval(window.slizg);
                that.oneIntervalStop = true;
                that.speed = 0;
              }
            } else {
              that.speed += that.friction
              if (that.speed >= 0) {
                clearInterval(window.var);
                that.oneIntervalStart = true;
                clearInterval(window.slizg);
                that.oneIntervalStop = true;
                that.speed = 0;
              }

            }
          }, 30)
        }
        this.oneIntervalStop = false;
      }
    }
  }
</script>

<style>
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 2s;
  }
  
  .fade-enter,
  .fade-leave-to
  /* .fade-leave-active below version 2.1.8 */
  
  {
    opacity: 0;
  }
  
  .display {
    white-space: nowrap;
    max-width: 100%;
  }
  
  .arrow {
    width: auto;
    height: 70px;
    margin: 20px;
    cursor: pointer;
  }
  
  .center-arrow {
    display: flex;
    justify-content: center;
  }
</style>
