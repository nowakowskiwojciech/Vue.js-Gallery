<template>
  <div>
    <div class='display'>
      <photo v-for="photo in photos" :styl="elPos" :url="photo" :key="photo">
      </photo>
    </div>
    <div style='display:flex; justify-content:center;'>
      <img src="../assets/arrow-l.png" class='arrow' @mouseover="startAnimation" @mouseleave="stopAnimation">
      <img src="../assets/arrow-r.png" class='arrow' @mouseover="startAnimation" @mouseleave="stopAnimation">
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
        oneIntervalStart: true,
        oneIntervalStop: true
      }
    },
    methods: {
      moveEl() {
        this.elX += this.speed;
        this.elPos = this.elX + 'px'
      },
      startAnimation() {
        if (this.oneIntervalStart == true) {
          window.var = setInterval(this.moveEl, 20);
          var that = this;
          window.el = setInterval(function() {
            that.speed += 0.2;
            if (that.speed >= 8) {
              clearInterval(window.el);
            }
          }, 30)
          this.oneIntervalStart = false;
        }
      },
      stopAnimation() {
        clearInterval(window.el);
  
        var that = this;
        if (this.oneIntervalStop == true) {
          window.slizg = setInterval(function() {
            that.speed -= 0.2
            if (that.speed <= 0) {
              clearInterval(window.var);
              that.oneIntervalStart = true;
              clearInterval(window.slizg);
              that.oneIntervalStop = true;
              that.speed = 0;
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
    transition: opacity 1.5s;
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
</style>
