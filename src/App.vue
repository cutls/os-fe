<template>
  <div id="app">
    <h1>OpenSticker</h1>
    <App/>
    <Introduction/>
    (c) 2020 weep, kyori19, cutls
  </div>
</template>

<script>
import App from './components/App'
import Introduction from './components/Introduction'

export default {
  name: 'Top',
  components: {
    App,
    Introduction
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
