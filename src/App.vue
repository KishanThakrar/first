<template>
  <div id="app">
    <HelloWorld msg="Calculator"/>
    <smitPage/>
    <kisuPage/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import SmitPage from './components/SmitPage.vue'
import KisuPage from './components/kisuPage.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    SmitPage,
    KisuPage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
