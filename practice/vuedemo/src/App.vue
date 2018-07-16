<template>
  <!-- 路由学习 -->
  <!--<div id="app">-->
    <!--<img src="./assets/logo.png">-->
    <!--<transition name="fade">-->
      <!--<keep-alive>-->
        <!--<router-view></router-view>-->
      <!--</keep-alive>-->
    <!--</transition>-->
    <!---->
    <!--<router-link :to="{path: '/apple'}" tag="li"> to apple</router-link>-->
    <!--<router-link :to="{name: 'bananaPage'}"> to banana</router-link>-->
    <!--<router-link :to="{path: '/apple/red'}"> to red aplle</router-link>-->
  <!--</div>-->

  <!-- vuex 学习 -->
  <div id="app">
    <img src="./assets/logo.png">
    {{ totalPrice }}
    <apple></apple>
    <banana></banana>
  </div>
</template>

<script>
  import Apple from './components/Apple'
  import Banana from './components/Banana'
export default {
  name: 'App',
  components: {Apple, Banana},
  computed: {
    totalPrice() {
      return this.$store.getters.getTotal;
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
