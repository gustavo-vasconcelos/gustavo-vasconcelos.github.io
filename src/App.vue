<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  
}
</script>

<style lang="scss">
@import "../src/assets/scss/index.scss";
@import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');

#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow-x: hidden;
}
</style>
