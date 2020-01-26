<template>
  <div id="app">
    <div id="image-wrapper" :style="{backgroundImage: `url(caterpillar.jpg)`}">
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
}
</script>

<style lang="scss" scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  #image-wrapper {
    height: 640px;
    background-repeat: no-repeat;
    position: relative;
    width: 640px;
  }
}
</style>
