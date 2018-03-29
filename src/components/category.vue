<template>
    <div>
        <div>
            <div class='row'>
                <transition  name="fade" >
                  <h1 v-if="show" @click="hide" align="left">Back</h1>
                </transition>
            </div>
        </div>
        <div class='display row'  >
          <transition-group name="fade">
              <photo v-if="show" v-for="photo in photos" :styl ="shift" :url="photo" :key="photo">
              </photo>
          </transition-group>
        </div>
          <div style='display:flex; justify-content:center;'>
          <transition name="fade">
            <span v-if="show" style='margin:20px; cursor:pointer; font-weight:bold' @mouseover="startAnimate" @mouseleave="stop"><-</span>
          </transition>
          <transition name="fade">
            <span v-if="show"  style='margin:20px; cursor:pointer; font-weight:bold' @mouseover="startAnimate" @mouseleave="stop">-></span>
          </transition>
          </div>
    </div>
</template>

<script>
import photo from '../components/photo'

export default {
  props:['show', 'photos'],
  name: 'Category',
  components: {
    photo
  },
  data () {
    return {
      photos: [1, 2, 3, 4],
      shift: 0,
      mouseX:0,
      x:0,
      friction:0,
      can: true,
      can2:true   }
  },
  methods: {
    display () {
      this.show = true
      
    },
    hide () {
      this.show = false
    },
    moveEl(){
      this.x+=this.friction;
      this.shift = this.x+'px'
    },
    startAnimate (){
      if(this.can == true){
        window.var = setInterval(this.moveEl,20);
        var that = this;
        window.el = setInterval(function(){
        that.friction += 0.2;
          if(that.friction >= 8){
            clearInterval(window.el);
          }
        },30)
        this.can = false;
      }
    }
    ,
    stop() {
      clearInterval(window.el);

      var that = this;
      if(this.can2 == true){
        window.slizg = setInterval(function(){
          that.friction -= 0.2
          if(that.friction <=0 ){
            clearInterval(window.var);
            that.can = true;
            clearInterval(window.slizg);
            that.can2 = true;
            that.friction = 0;
          }
        },30)
    }
    this.can2 = false;

    }
  }
}


</script>
<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 2s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.display {
  white-space:nowrap;
  max-width: 100%;

}
body {
  overflow:hidden
}
</style>
