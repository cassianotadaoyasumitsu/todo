<template>
  <div id="app" class="container">
    <img src="./assets/kamon.jpg">
    <ToDo></ToDo>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import ToDo from './components/Todo'

export default {
  name: 'App',
  components: {
    HelloWorld,
    ToDo,
  }
}
</script>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  max-width: 600px;
  margin: 0 auto;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 16px;
}
</style>
