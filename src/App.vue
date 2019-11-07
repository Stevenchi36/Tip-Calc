<template>
  <div id="app">
    <h1>Tip Calculator</h1>
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'app',
  components: {
    Calculator
  }
}
</script>

<style>
html {
  font-size: 1.2rem;
  background-color: rgb(188, 255, 255);
  background-image: linear-gradient(to bottom right, rgb(174, 225, 255), rgb(180, 255, 184));
  background-repeat: no-repeat;
  min-height: 100vh;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #040027;
  margin-top: 3rem;
  line-height: 1.5;
}
</style>
