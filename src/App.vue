<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">

    <TextCustom>Lorem ipsum dolor.</TextCustom>
    <Rectangle></Rectangle>
    <Rectangle></Rectangle>
  </div>
</template>

<script>
import Rectangle from './components/Elements/Rectangle';
import TextCustom from './components/Elements/TextCustom';

export default {
  name: 'app',
  components: {
    Rectangle,
    TextCustom
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
