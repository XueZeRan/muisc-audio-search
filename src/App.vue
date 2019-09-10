<template>
  <div id="app">
    <div class="container">
      <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
        <!-- <a class="a-btn navbar-brand" to="/">music-Search</a> -->
        <router-link class="a-btn" to="/">music-Search</router-link>
        <router-link class="a-btn" to="/au">电影</router-link>
      </nav>       
    </div>
    <keep-alive><router-view></router-view></keep-alive>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style lang='stylus' scoped>
  a
    color #fff
  .a-btn
    padding 0 10px 0 10px
  .a-btn:hover
    padding 5px
    background #fff   /* 鼠标移动到链接上 */
    border-radius 10px
  .router-link-exact-active
    background #0555ad
    padding 5px
    border-radius 10px
</style>
