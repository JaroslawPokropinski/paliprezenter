<template>
  <div id="app">
    <Builder />
  </div>
</template>

<script>
import Builder from './components/Builder'

export default {
  name: 'app',
  components: {
    Builder
  }
}
</script>

<style>
html, body {
  height: 100%;
  margin: 0;
  padding: 0;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0;
  background-color: #141d26;
  height: 100%;
  overflow: hidden;
}
</style>
