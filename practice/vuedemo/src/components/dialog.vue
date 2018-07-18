<template>
  <div>
    <div class="dialog-wrap" v-if="isShow">
        <div class="dialog-cover" v-if="isShow" @click="closeMyself"></div>
      <!-- transition要紧跟v-if-->
      <transition name="drop">
        <div class="dialog-content"  v-if="isShow">
          <p class="dialog-close" @click="closeMyself">X</p>
          <slot>empty</slot>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
   export default {
     props: {
       isShow: {
         type: Boolean,
         default: false
       }
     },
     data() {
       return {

       }
     },
     methods: {
       closeMyself() {
         this.$emit('on-close')
       }
     }
   }

</script>

<style scoped>
  .drop-enter-active {
    transition: all .5s ease;
  }
  .drop-leave-active {
    transition: all .3s ease;
  }
  .drop-enter {
    transform: translateY(-500px);
  }
  .drop-leave-active {
    transform: translateY(-500px);
  }

  .dialog-wrap {
    position: fixed;
    width: 100%;
    height: 100%;
  }

  .dialog-cover {
    background: #000;
    opacity: 0.3;
    position: fixed;
    z-index: 5;
    top:0;
    left: 0;
    width: 100%;
    height: 100%;
  }

  .dialog-content {
    width: 40%;
    min-width: 600px;
    position: fixed;
    max-height: 50%;
    overflow: auto;
    background: #FFF;
    top:20%;
    left: 60%;
    margin-left: -30%;
    z-index: 10;
    border: 2px solid #464068;
    padding: 2%;
    line-height: 1.6;
  }

  .dialog-close {
    position: absolute;
    right: 10px;
    top:5px;
    font-size: 20px;
  }
</style>
